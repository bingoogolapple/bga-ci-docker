FROM openjdk:8-jdk-alpine
LABEL maintainer="bingoogolapple@gmail.com"

USER root

# 设置环境变量
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_ROOT /opt/android-sdk-linux
ENV ANDROID_SDK /opt/android-sdk-linux
ENV NDK_ROOT /opt/android-sdk-linux/ndk-bundle
ENV PATH ${PATH}:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/proguard/bin:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/emulator:${ANDROID_HOME}/bin:${NDK_ROOT}

ARG GLIBC_VERSION="2.28-r0"

RUN echo "使用清华大学镜像安装依赖" \
  && echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/main" > /etc/apk/repositories \
  && echo "https://mirrors.tuna.tsinghua.edu.cn/alpine/latest-stable/community" >> /etc/apk/repositories \
  && apk -U --no-cache --allow-untrusted add \
  bash \
  ca-certificates \
  curl \
  expect \
  git \
  make \
  libstdc++ \
  libgcc \
  su-exec \
  ncurses \
  unzip \
  wget \
  zlib \
  && wget https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -O /etc/apk/keys/sgerrand.rsa.pub \
  && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk -O /tmp/glibc.apk \
  && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk -O /tmp/glibc-bin.apk \
  && apk add /tmp/glibc.apk /tmp/glibc-bin.apk \
  && rm -rf /tmp/* \
  && rm -rf /var/cache/apk/* \
  && echo "下载 Android SDK Tools https://developer.android.com/studio/#downloads" \
  && mkdir -p $ANDROID_HOME \
  && wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O sdk-tools-linux.zip \
  && unzip sdk-tools-linux.zip -d $ANDROID_HOME \
  && rm -rf sdk-tools-linux.zip \
  && echo "配置 sdkmanager https://developer.android.com/studio/command-line/sdkmanager" \
  && mkdir $ANDROID_HOME/licenses || true \
  && echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > $ANDROID_HOME/licenses/android-sdk-license \
  && echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > $ANDROID_HOME/licenses/android-sdk-preview-license \
  && mkdir ~/.android \
  && touch ~/.android/repositories.cfg \
  && mkdir $ANDROID_HOME/.android \
  && touch $ANDROID_HOME/.android/repositories.cfg \
  && sdkmanager --version && echo y | sdkmanager --update && echo y | sdkmanager --licenses \
  && echo "下载 Android SDK" \
  && echo y | sdkmanager "platform-tools" \
  && echo y | sdkmanager "tools" \
  && echo y | sdkmanager "extras;android;m2repository" \
  && echo y | sdkmanager "extras;google;m2repository" \
  && echo y | sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" \
  && echo y | sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2" \
  && echo y | sdkmanager "build-tools;28.0.3" \
  && echo y | sdkmanager "platforms;android-28"
#   && echo y | sdkmanager "cmake;3.6.4111459" \
#   && echo y | sdkmanager "ndk-bundle" 