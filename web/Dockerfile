FROM ubuntu:14.04

MAINTAINER alexander@spetko-it-consulting.eu

# setup proxy here if needed...

############################
## Install unzip and wget ##
############################
RUN apt-get update \
 && apt-get install -y wget unzip

##################################
## Downloading and install Java ##
##################################
RUN cd /tmp \
 && wget -c --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"-O http://download.oracle.com/otn-pub/java/jdk/8u92-b14/jdk-8u92-linux-x64.tar.gz \ 
 && cd /opt/ \
 && tar xzvf /tmp/jdk-8u92-linux-x64.tar.gz \
 && rm -f /tmp/jdk-8u92-linux-x64.tar.gz

###########################
## Downloading Glassfish ##
###########################
RUN cd /tmp \
 && wget -c http://download.oracle.com/glassfish/4.1.1/release/glassfish-4.1.1-web.zip

#############################
## Create a glassfish user ##
#############################
RUN adduser glassfish --home /opt/glassfish4/ --shell /bin/bash 

###########################################
## Install glassfish and remove zip file ##
###########################################
RUN cd /tmp \
 && unzip glassfish-4.1.1-web.zip -d /opt\
 && rm glassfish-4.1.1-web.zip

############################################
## Change the right to the glassfish user ##
############################################
RUN chown -R glassfish /opt/glassfish4/

#################################################
## Add the startup script and make it runnable ##
#################################################
ADD run.sh /opt/run.sh
RUN mv /opt/run.sh /opt/glassfish4/run.sh \
 && chown glassfish /opt/glassfish4/run.sh && chmod 777 /opt/glassfish4/run.sh

#############################
## Default glassfish ports ##
#############################
EXPOSE 4848 8080 8181

###################################
## User: admin / Pass: glassfish ##
###################################
RUN echo "admin;{SSHA256}80e0NeB6XBWXsIPa7pT54D9JZ5DR5hGQV1kN1OAsgJePNXY6Pl0EIw==;asadmin" > /opt/glassfish4/glassfish/domains/domain1/config/admin-keyfile
RUN echo "AS_ADMIN_PASSWORD=glassfish" > /opt/glassfish4/pwdfile

###################################################
## Set glassfish user in its home/bin by default ##
###################################################
USER glassfish
WORKDIR /opt/glassfish4/bin

###################################
## Set the path to the JAVA_HOME ##
###################################
RUN echo "export PATH=$PATH:/opt/glassfish4/bin:/opt/jdk1.8.0_92/bin" >> /opt/glassfish4/.bashrc 

#######################################
## Final configuration for glassfish ##
#######################################
RUN export PATH=$PATH:/opt/glassfish4/bin:/opt/jdk1.8.0_92/bin \ 
 && ./asadmin start-domain \
 && ./asadmin --user admin --passwordfile /opt/glassfish4/pwdfile enable-secure-admin \
 && ./asadmin stop-domain

##############################################
## Default command to run on container boot ##
##############################################
CMD ["/opt/glassfish4/run.sh"]
