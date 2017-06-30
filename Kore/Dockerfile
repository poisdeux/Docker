FROM ubuntu:16.04

MAINTAINER Martijn Brekhof "m.brekhof@gmail.com"

ENV ANDROID_HOME /opt/android-sdk-linux


# ------------------------------------------------------
# --- Install required tools

RUN apt-get update -qq

# Dependencies to execute Android builds
RUN apt-get install -y openjdk-8-jdk wget expect unzip git

WORKDIR /opt/
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip

ENV PATH ${PATH}:/opt/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

RUN mkdir ${ANDROID_HOME}
WORKDIR ${ANDROID_HOME}
RUN unzip /opt/sdk-tools-linux-3859397.zip
RUN bash -c 'echo -e "y\ny\ny\ny\ny\ny\ny\n" | sdkmanager --licenses'
RUN sdkmanager "platforms;android-25"
RUN sdkmanager "platform-tools"
RUN sdkmanager "build-tools;25.0.2"
RUN sdkmanager "extras;google;m2repository"
RUN sdkmanager "extras;android;m2repository"
RUN sdkmanager "system-images;android-25;google_apis;x86_64"
RUN sdkmanager "emulator"

WORKDIR /opt
RUN git clone https://github.com/xbmc/Kore.git
WORKDIR /opt/Kore
#Load project dependencies
RUN ./gradlew

#Create an android emulator. Not needed as our instrumented tests fail on a headless emulator
#RUN echo no | avdmanager create avd -n "Nexus_5_API_25" --package "system-images;android-25;google_apis;x86_64" --tag "google_apis"

RUN apt-get clean
