Sonar & Nexus - t2.med, Jenkins - t2.large

sudo apt update - 3
Jenkins:
install java17
chrome: jenkins on ubuntu/latest release
sudo cat /var - get pwd and open Jenkins dashboard
install docker
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance)

sonarqube:
install docker
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance)
sudo docker run -itd -p 9000:9000 sonarqube:latest

Nexus:
install docker
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance)
sudo docker run -itd -p 8081:8081 sonatype/nexus3
