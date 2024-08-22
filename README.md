Sonar & Nexus - t2.med, Jenkins - t2.large

sudo apt update - all 3

Jenkins: \
install java17 \
chrome: jenkins on ubuntu/latest release \
sudo cat /var - get pwd and open Jenkins dashboard \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need to mention sudo at every instance) \
install trivy \

sonarqube: \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need to mention sudo at every instance) \
docker run -itd -p 9000:9000 sonarqube:lts-community \
docker ps \
chrome: publicIP:9000 (default: admin/admin, new pwd) \
generate token \

Nexus: \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need to mention sudo at every instance) \
docker run -itd -p 8081:8081 sonatype/nexus3 \
docker ps \
chrome: publicIP:8081 (default: admin/for pwd .. need to enter into container) \
docker exec -it containedID /bin/bash \
cat sonatype-work/nexus3/admin.password (copy pwd and later change) \

Jenkins Dashboard:

manage jenkins/plugins/available plugins \

SonarQube Scanner \
Maven Integration \
Pipeline Maven Integration \
Config File Provider (for Nexus) \
Kubernetes \
Kubernetes credentials \
Kubernetes CLI \
Kubernetes Client API \
Docker \
Docker Pipeline \
Pipeline Stage View \
Eclipse Temurin Installer (for java 17) \

(once plugins are installed, we need to configure)

Tools Configuration: 4
manage jenkins/tools

1.Docker:
name: docker
click install automatically
download from docker.com/docker version:latest

2.Maven:
name: maven3
version: no change

3.SonarQube Scanner installations:
name: sonar-scanner
version: no change

4.JDK installations:
(we are using jdk17, incase we want to use another jdk -- install plugin "Eclipse Temurin Installer")
name: jdk17
click install automatically/Install from adoptium.net/version: jdk-17.0.11+9

Credentials: 1
manage jenkins/credentials/global/add
git-cred: (secret text - needs token, if repo is in private)
1.sonar-cred: (secret text - needs token)

Servers Configuration: 1
manage jenkins/system

1.Sonarqube servers/add sonarqube
name: sonar-server
url: http://3.27.232.79:9000
select token

Store Artifacts: 1
manage jenkins/managed files

add a new config/select "Global Maven settings.xml"/ID: maven-settings/next

add 2 servers in servers section

<server>
	<id>maven-releases</id>
      	<username>admin</username>
      	<password>nexus</password>
</server>
	
<server>
      	<id>maven-snapshots</id>
      	<username>admin</username>
      	<password>nexus</password>
</server>

then, submit (we can communicate with Nexus)

Dashboard: new item: Blogging-App/pipeline

Discard Old Builds: Max - 2

steps in building pipeline

change url in pom.xml for releases and snapshots








