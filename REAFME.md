#!/bin/bash
# Author : Geovanie I.
# Date : 04/02/2022
# Description : Jenkins Installation on Centos7

echo "Step 1: Install Java"
 sudo yum install wget -y
 sudo yum install java-1.8.0-openjdk-devel
echo "Step 2: Enable the Jenkins repository"
 sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
if
 [ $? ne 0 ]
then
echo " installation failed "

 else
   [ $? eq 0 ]
 sudo sed -i 's/gpgcheck=1/gpgcheck=0/g' /etc/yum.repos.d/jenkins.repo
 if
 [ $? ne 0 ]
then
echo " installation failed "

 else
   [ $? eq 0 ]
 sudo sed -i 's/gpgcheck=1/gpgcheck=0/g' /etc/yum.repos.d/jenkins.repo

echo " Step 3: Install the latest stable version of Jenkins "
 sudo yum install jenkins
 sudo systemctl start jenkins
 sudo systemctl status jenkins
echo " enable the Jenkins service to start on system boot "
 sudo systemctl enable jenkins
echo " Step 4: Adjust the firewall "
 sudo firewall-cmd --permanent --zone=public --add-port=8080/tcp
 sudo firewall-cmd --reload
echo
echo " Open the jenkins page from the browser "
echo " Launch your google chrome browser an type your IP address followed by the port number 8080 "
echo " ipaddr=`hostname -I |awk '{print$2}' "
fi