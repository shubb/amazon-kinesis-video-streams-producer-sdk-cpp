FROM ubuntu:18.04

RUN apt-get upgrade
RUN apt-get update

RUN apt-get install -y git && \
    apt-get install -y vim  && \
    apt-get install -y curl && \
    apt-get install -y xz-utils && \
    apt-get install -y byacc  && \
    apt-get install -y wget  && \
    apt-get install -y g++ && \
    apt-get install -y python2.7 && \
    apt-get install -y pkg-config && \
    apt-get install -y cmake && \
    apt-get install -y maven && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y python && \
    apt-get install -y python-dev && \
    rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/
WORKDIR /opt/

# ===== Git Checkout latest Kinesis Video Streams Producer SDK (CPP) =======================================

RUN git clone https://github.com/shubb/amazon-kinesis-video-streams-producer-sdk-cpp.git

# ================ Build the Producer SDK (CPP) ============================================================

WORKDIR /opt/amazon-kinesis-video-streams-producer-sdk-cpp/kinesis-video-native-build/
RUN  chmod a+x ./install-script
