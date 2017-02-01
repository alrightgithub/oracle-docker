# LICENSE MIT 2017
#
# --------------------------------------
# alrightgithub's oracle docker projects
# --------------------------------------
# This is the Dockerfile for an installation of Oracle Java JDK7 on OEL (latest)
#
# AUTHOR
# ---------------------------
# Dan U (dan@alrightmate.com)
# ---------------------------
# 
# FILES REQUIRED TO BUILD
# -----------------------
# server-jre-7u*-linux-x64.tar.gz (Oracle Java SE 7 for Linux x64)
#
# Usage:
# ------
# Put downloaded files in the same directory as this Dockerfile
# 
# build:  docker build -t alrightgithub/oelserverjdk7 .
# run: docker run -it alrightgithub/oelserverjdk7

FROM oraclelinux:latest

# Set our ENV vars
ENV JAVA_PKG=server-jre-7u*-linux-x64.tar.gz \
    JAVA_HOME=/usr/java/default

# Install & configure Java
ADD $JAVA_PKG /usr/java/
RUN export JAVA_DIR=$(ls -1 -d /usr/java/*) && \
    ln -s $JAVA_DIR /usr/java/latest && \
    ln -s $JAVA_DIR /usr/java/default && \
    alternatives --install /usr/bin/java java $JAVA_DIR/bin/java 20000 && \
    alternatives --install /usr/bin/javac javac $JAVA_DIR/bin/javac 20000 && \
    alternatives --install /usr/bin/jar jar $JAVA_DIR/bin/jar 20000
