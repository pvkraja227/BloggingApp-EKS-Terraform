pipeline { 
    agent any
    
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    environment {
        SCANNER_HOME= tool "sonar-scanner"
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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                sh ''' $SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=Blogging-app -Dsonar.projectKey=Blogging-App -Dsonar.java.binaries=target '''
                }
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }

        stage('Package') {
            steps {
                sh "mvn package"
            }
        }
    }
}
