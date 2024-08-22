Sonar & Nexus - t2.med, Jenkins - t2.large

sudo apt update - 3

Jenkins: \
install java17 \
chrome: jenkins on ubuntu/latest release \
sudo cat /var - get pwd and open Jenkins dashboard \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance)

sonarqube: \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance) \
docker run -itd -p 9000:9000 sonarqube:lts-community \
docker ps \
chrome: publicIP:9000 (default: admin/admin, new pwd) \
generate token \

Nexus: \
install docker \
sudo chmod 666 /var/run/docker.sock (one time permission to all users to use docker or else we need mention sudo at every instance) \
docker run -itd -p 8081:8081 sonatype/nexus3 \
docker ps \
chrome: publicIP:8081 (default: admin/for pwd .. need to enter into container) \
docker exec -it containedID /bin/bash \
cat sonatype-work/nexus3/admin.password (copy pwd and later change) \
