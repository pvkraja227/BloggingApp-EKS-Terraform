pipeline { 
    agent any
    
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }
    
    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/pvkraja227/BloggingApp-EKS-Terraform.git'        
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('Trivy FS Scan') {
            steps {
                sh "trivy fs --format table -o fs.html ."
            }
        }

        stage('Build') {
            steps {
                sh "mvn package"
            }
        }

        stage('Publish Artifacts') {
            steps {
                withMaven(globalMavenSettingsConfig: 'maven-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                sh "mvn deploy"
                }
                
            }
        }
        
        stage('Docker Build & Tag') {
            steps {
                script {
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                
                sh "docker build -t rajapvk23/blogging-apps:latest ."    
                }
                }
            }
        }
        
        stage('Trivy Image Scan') {
            steps {
                sh "trivy image --format table -o image.html rajapvk23/blogging-apps:latest"
            }
        }
        
        stage('Docker Push') {
            steps {
                script {
                withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                
                sh "docker push rajapvk23/blogging-apps:latest"    
                }
                }
            }
        }
        
        stage('k8-Deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'devopsshack-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://5A2F1C9F022B77CE670614A08A5CFF2D.gr7.ap-southeast-2.eks.amazonaws.com') {
                    sh "kubectl apply -f deployment-service.yml" 
                    sleep 5
                }    
            }
        }
        
        stage('Verify Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'devopsshack-cluster', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://5A2F1C9F022B77CE670614A08A5CFF2D.gr7.ap-southeast-2.eks.amazonaws.com') {
                    sh "kubectl get pods"
                    sh "kubectl get svc"
                    
                }    
            }
        }
    }
}
