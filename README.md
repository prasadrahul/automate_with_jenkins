# automate_with_jenkins
Demo on Continuous integration with Jenkins

# Install Java

```
sudo apt-get install -y wget apt-transport-https gnupg
wget https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public
gpg --no-default-keyring --keyring ./adoptopenjdk-keyring.gpg --import public
gpg --no-default-keyring --keyring ./adoptopenjdk-keyring.gpg --export --output adoptopenjdk-archive-keyring.gpg
rm adoptopenjdk-keyring.gpg
sudo mv adoptopenjdk-archive-keyring.gpg /usr/share/keyrings && sudo chown root:root /usr/share/keyrings/adoptopenjdk-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/adoptopenjdk-archive-keyring.gpg] https://adoptopenjdk.jfrog.io/adoptopenjdk/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/adoptopenjdk.list
sudo apt-get update
sudo apt-cache search adoptopenjdk
sudo apt-get install adoptopenjdk-11-hotspot
sudo echo "/usr/lib/jvm/adoptopenjdk-11-hotspot-amd64/" >> /etc/environment
```

# Install Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

```

# Install Maven

```
sudo apt-get install maven
```
# Install Ant
```
sudo apt-get install ant
```

# Configure Jenkins

``` 
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
<random-password-for-intial-configuration>

# Access Jenkins at 8080 port ( default port )

# Configure Global Tool Configuration for JDK/Maven/Ant
```

# Setup dev and prod instance

```
cd $HOME
mkdir AUTOMATE_WITH_JENKINS
cd AUTOMATE_WITH_JENKINS/
wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.0.12/bin/apache-tomcat-10.0.12.tar.gz
tar -xvf apache-tomcat-10.0.12.tar.gz 
mv apache-tomcat-10.0.12 dev_tomcat
tar -xvf apache-tomcat-10.0.12.tar.gz 
mv apache-tomcat-10.0.12 prod_tomcat
sed -i 's/8005/9005/g' $HOME/AUTOMATE_WITH_JENKINS/dev_tomcat/conf/server.xml
sed -i 's/8080/9000/g' $HOME/AUTOMATE_WITH_JENKINS/dev_tomcat/conf/server.xml
sed -i 's/8443/9443/g' $HOME/AUTOMATE_WITH_JENKINS/dev_tomcat/conf/server.xml
sed -i 's/8080/8000/g' $HOME/AUTOMATE_WITH_JENKINS/prod_tomcat/conf/server.xml
cd $HOME/AUTOMATE_WITH_JENKINS/dev_tomcat/bin
./startup.sh
cd $HOME/AUTOMATE_WITH_JENKINS/prod_tomcat/bin
./startup.sh
```

# Install Docker
