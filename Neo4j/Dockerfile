########## Dockerfile for Neo4j version 3.2.6 ##################################
#
# This Dockerfile builds a basic installation of Neo4j.
#
# Neo4j is the world's leading Graph Database.Neo4j is available both as a standalone server, or an embeddable component.  
# It is a high performance graph store with all the features expected of a mature and robust database, like a friendly query language and ACID transactions.
#
# To build this image, from the directory containing this Dockerfile
# (assuming that the file is named Dockerfile):
# docker build -t <image_name> .
#
# To simply run the resultant image, and provide a bash shell:
# docker run -it <image_name> /bin/bash
# 
# Start neo4j server using below command:
# docker run <container_name> -d -p <host-port>:<container-port> -v /<host>:/<container> <image-name> neo4j <command>
# e.g. docker run --name Neo4j -d -p 9095:7474 -v /root:/root/ neo4j_img neo4j start 
#
# Official website: https://neo4j.com/
#
##################################################################################

#Base Image
FROM s390x/ubuntu:16.04

# The author
MAINTAINER  LoZ Open Source Ecosystem (https://www.ibm.com/developerworks/community/groups/community/lozopensource)

ENV SOURCE_DIR='/root'

ENV NEO4J_HOME=$SOURCE_DIR/neo4j
ENV JAVA_HOME=$SOURCE_DIR/jdk-9+181
ENV PATH=$PATH:$NEO4J_HOME/bin:$JAVA_HOME/bin

WORKDIR $SOURCE_DIR

# Install dependencies
RUN  apt-get update  \
  && apt-get install -y  \
                tar \
                wget \

# Download adoptopenjdk
  && cd $SOURCE_DIR/ \
  && wget https://github.com/AdoptOpenJDK/openjdk9-releases/releases/download/jdk-9%2B181/OpenJDK9_s390x_Linux_jdk-9.181.tar.gz \
  && tar -xvzf OpenJDK9_s390x_Linux_jdk-9.181.tar.gz \

# Download and unzip Neo4j pre build Binary
  && cd $SOURCE_DIR/ \
  && wget https://neo4j.com/artifact.php?name=neo4j-community-3.2.6-unix.tar.gz \
  && tar -xvzf artifact.php?name=neo4j-community-3.2.6-unix.tar.gz \
  && mv neo4j-community-3.2.6 neo4j \

# Clean up the unwanted packages and clear the source directory
  && apt-get remove -y \
                wget  \
  && apt-get autoremove -y \
  && apt autoremove -y \
  && apt-get clean \
  && rm -rf $SOURCE_DIR/OpenJDK9_s390x_Linux_jdk-9.181.tar.gz $SOURCE_DIR/artifact.php?name=neo4j-community-3.2.6-unix.tar.gz /var/lib/apt/lists/*

VOLUME /data

# Port for Neo4j
EXPOSE 7474 7473 6362 5000 6000 7000 5001 6001 2003 3637 1337

# Set the Entrypoint
CMD ["neo4j"]

# End of Dockerfile