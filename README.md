# AWS_CFT
cloudformationtemplate
CI/CD Pipeline Build
  AWS AMI instance
  Java and Jenkins configuration
  Install all required plugins
  Install and configure Ansible servers
  Configure Git (Bitbucket)
  



Check Java version
      java -version
      yum remove java-1.7.0*
      java -version
	  
Download new JDK/JRE files
    mv jdk-11.0.8_linux-x64_bin.tar.gz /usr/lib/jvm
    ls -ltr
    cd /usr/lib/jvm
    sudo tar -xvzf jdk-11.0.8_linux-x64_bin.tar.gz
   
   
cd etc/ and add Java home and Path
       PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/lib/jvm/jdk-11.0.8/bin"
       JAVA_HOME="/usr/lib/jvm/jdk-11.0.8"
       nano environment
      cat environment
      sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-11.0.8/bin/java" 0
      sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk-11.0.8/bin/javac" 0
      sudo update-alternatives --set java /usr/lib/jvm/jdk-11.0.8/bin/java
      sudo update-alternatives --set javac /usr/lib/jvm/jdk-11.0.8/bin/javac
      update-alternatives --list java
      sudo update-alternatives --config java
      sudo update-alternatives --config javac
      java -version
    
     reboot
     yum install update -y
   
Edit .bash_profile to add JAVA_HOME path
   
     vi .bash_profile
     echo $JAVA_HOME
	 
Install Jenkins.	 
     yum jenkins install -y
     sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
     sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
     yum install jenkins -y
     jenkins service status
     service jenkins status
     service jenkins start
     service jenkins status
    
Copy the ec2 <ip>:8080
	Jenkins password
    cat /var/lib/jenkins/secrets/initialAdminPassword
	http://54.144.0.252:8080/

Configure Jenkins
  Managed Jenkins ==> Global Tool Configuration ==>add java home
  $echo JAVA_HOME
  ->Copy output to jenkins dashboard.
  
Install and setup Git on the EC2 Jenkins servers
  Yum install jenkins -y

Install Plugins  
  Bitbucket plugins
  Github plugins
  Blue ocean plugins
  Maven plugins
  
Install Maven
  cd /opt/
yum install wget  
   wget https://mirrors.sonic.net/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz  
   tar -xvzf apache-maven-3.6.3-bin.tar.gz
   ls -ltr
   mv apache-maven-3.6.3 apache-maven
   cp apache-maven apache-maven-3.6.3
   cp -R  apache-maven apache-maven-3.6.3
   
Edit the bash_profile and add maven home

   M2_HOME=/opt/apache-maven
   M2=/opt/apache-maven/bin
   sudo yum update
   hostname <any name>
   mvn -v or mvn --version

Configure Maven on Jenkins
   Install Maven plugins
   Go to Global tool configuration
    search for Maven and configure details   
  
Installing Ansible ==>Use for deploying code to the UAT/PROD env'ts
  Using Amazon ec2 instance.
Installing docker Pre-requisites

Amazon Linux EC2 Instance

Installation Steps
     Install docker and start docker services
yum install docker -y
docker --version 

Star docker deamon
  service docker start
  service docker status
  
Create a user called dockeradmin

useradd dockeradmin
passwd dockeradmin

add a user to docker group to manage docker
usermod -aG docker dockeradmin  
 
Plugins
  Publish Over SSH

Issue
￼Failed to connect to repository : Command "git ls-remote -h -- http://bitbucket.cgif-hcp.com/scm/pecos2/new-hire-pocs.git HEAD" returned status code 128:
stdout:
stderr: fatal: unable to access 'http://bitbucket.cgif-hcp.com/scm/pecos2/new-hire-pocs.git/': SSL certificate problem: unable to get local issuer certificate

Solution:
git config --global http.sslVerify false
git config --list
 
	
    
