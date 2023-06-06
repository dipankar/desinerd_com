---
slug: "installing-solr-tomcat-on-rhel5"
title: Installing Solr + Tomcat on RHEL5
date: "2010-03-31"
tags: ['drupal', 'index', 'integration', 'rhel5', 'search', 'solr', 'tomcat']
---
Installing JDK

Download the latest Sun JDK RPM.
Go to java.sun.com and navigate to the downloads page. As of this writing it is http://java.sun.com/javase/downloads/index.jsp
	If you are on a text console, you may want to use the “links” text browser rather than wget or curl. The Sun site requires you to accept a license agreement before it will allow you to access the download.
	Navigate to the downloads for a recent version of the JDK (e.g. JDK 6 update 2).
	On the downloads page, download the “Linux RPM in self-extracting file” This will have a name such as jdk-6u2-linux-i586-rpm.bin
	Save the file in a convient location (/tmp would work).

Extract and install the RPM
In the directory that you saved the rpm.bin file, type:
./jdk-6u2-linux-i586-rpm.bin

	The JDK should extract and install. There is a licence agreement.
Installing Tomcat

First, download Tomcat from Apache or a mirror site and unpack it.

Next you need to decide where to put Tomcat. You will need a directory for your Tomcat installation and also a place to store your Tomcat applications. This can be the same directory, but does not have to be. The method that I will illustrate here uses /opt/mytomcat for both directories

Often you may need to refer to the directory in which Tomcat is installed. This is stored in the environment variable $CATALINA_HOME (Catalina is Tomcat’s servlet container). Thus, by installing Tomcat into /opt/mytomcat, we can consider /opt/mytomcat to be $CATALINA_HOME.
ln -s /opt/apache-tomcat-5.5.23 /opt/mytomcat
Next, you need to decide how you will run Tomcat. Tomcat can be run as root or as a regular user. For security reasons, many people prefer to create a special user account to run Tomcat and to own Tomcat files. In this example, I will show how to set up a ‘mytomcat’ user. You’ll need to do most of the installation and setup as root and can then chown files to be owned by the mytomcat user.
/usr/sbin/groupadd mytomcat
/usr/sbin/useradd -g mytomcat -d /opt/mytomcat mytomcat
Change the directory to be owned by the mytomcat user (and also group mytomcat):
chown mytomcat.mytomcat mytomcat
chown mytomcat.mytomcat apache-tomcat-5.5.23
In order for Tomcat to find the installation of Java, you need to set the JAVA_HOME environment variable. One way to do this is to create a file $CATALINA_HOME/bin/setenv.sh that contains the following line:
JAVA_HOME="/usr/java/latest"
At this point, we should be able to try starting Tomcat. Since you are probably root, but we want to run Tomcat as user ''mytomcat’, use ''su -c’ to run the startup.sh script:
su mytomcat -c $CATALINA_HOME/bin/startup.sh
If everything worked, you should be able to navigate to http://localhost:8080 and see the Tomcat welcome page.
To stop the server, use:
su mytomcat -c $CATALINA_HOME/bin/shutdown.sh
Installing Solr

Download SOLR from Apache or a mirror, unpack it, and set up a link to it from /opt/solr.
cd /opt
wget ftp://www.ibiblio.org/pub/mirrors/apache/lucene/solr/1.2/apache-solr-1.2.0.tgz
tar xvzf apache-solr-1.2.0.tgz
ln -s apache-solr-1.2.0.tgz /opt/solr
Change the ownership and group to be mytomcat:
chown -R mytomcat:mytomcat solr
chown -R mytomcat:mytomcat apache-solr-1.2.0
Make a copy of a SOLR webapp. SOLR instances run as web applications in the webapps directory of Tomcat. There is a default application in /opt/solr/dist that is packaged as a .war file. To use this, just copy it over to /opt/mytomcat/webapps and give it a descriptive name:
cp /opt/solr/dist/apache-solr-1.2.0.war /opt/mytomcat/webapps/mytestapp.war
chown mytomcat:mytomcat /opt/mytomcat/webapps/mytestapp.war
SOLR stores its indicies for each instance in a “solr/home” directory. For SOLR webapps that you run, you will need to create a solr/home directory. I put all mine in /opt/solr_home, so that I have directories like /opt/solr_home/app1, /opt/solr_home/app2,… There is a sample directory that you should copy that contains the starting files and directories that SOLR expects for the solr/home:
mkdir /opt/solr_home
cp -R /opt/solr/example/solr /opt/solr_home/mytestapp
chown -R mytomcat:mytomcat /opt/solr_home

Works very well and rather straight out of the box.

All the credit goes to Robert - http://www.ils.unc.edu/~rcapra/rhel5-tomcat-solr.php

The above guide with some minor changes here and there.
