# LICENSE MIT 2017
#
# --------------------------------------
# alrightgithub's oracle docker projects
# --------------------------------------
# This is the Dockerfile for an installation of Oracle WLS 10.3.6 (11g) Generic on OEL with JDK7 already installed
# This doesn't create any WLS domains - it's an install of the product only
#
# AUTHOR
# ---------------------------
# Dan U (dan@alrightmate.com)
# ---------------------------
# 
# FILES REQUIRED TO BUILD
# -----------------------
# wls1036_generic.jar (Oracle WebLogic Server 10.3.6 Generic Installer)
# A built alrightgithub/oelserverjdk7 image
#
# Usage:
# ------
# Put downloaded files in the same directory as this Dockerfile
# Ensure you've built the alrightgithub/oelserverjdk7 image
# 
# build:  docker build -t alrightgithub/jdk7-wls1036 .
# run: docker run -it alrightgithub/jdk7-wls1036

FROM alrightgithub/oelserverjdk7:latest

# ENV vars required
# -----------------
ENV WLS_PKG wls1036_generic.jar
ENV JAVA_HOME /usr/java/default

# Create u01 dir and oracle user
# ------------------------------
RUN mkdir /u01 && \
    chmod a+xr /u01 && \
    useradd -b /u01 -m -s /bin/bash oracle 

# Copy required installer files
COPY $WLS_PKG /u01/
COPY wls-silent.xml /u01/

# Adjust file permissions, go to /u01 as user 'oracle'
RUN chown oracle:oracle -R /u01
WORKDIR /u01
USER oracle

# Install WLS using silent file
RUN java -jar $WLS_PKG -mode=silent -silent_xml=/u01/wls-silent.xml && \ 
	rm $WLS_PKG /u01/wls-silent.xml 

WORKDIR /u01/oracle/

ENV PATH $PATH:/u01/oracle/weblogic/oracle_common/common/bin

# Define default command to start bash. 
CMD ["bash"]