#============================================
# Flutter + Android SDK для GitHub Codespaces
#============================================

FROM mcr.microsoft.com/devcontainers/base:jammy

# Установка зависимостей + OpenJDK (обязательно для sdkmanager!)
RUN apt-get update && apt-get install -y \
    git \
    wget \
    unzip \
    libglu1-mesa \
    xvfb \
    curl \
    openjdk-11-jdk \
    && rm -rf /var/lib/apt/lists/*

# Установка Flutter
ENV FLUTTER_HOME=/opt/flutter
ENV PATH=${FLUTTER_HOME}/bin:${PATH}

RUN git clone https://github.com/flutter/flutter.git -b stable ${FLUTTER_HOME}

# Установка Android SDK
ENV ANDROID_HOME=/opt/android-sdk
ENV PATH=${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/emulator:${ANDROID_HOME}/platform-tools:${PATH}

RUN mkdir -p ${ANDROID_HOME}/cmdline-tools && \
    cd ${ANDROID_HOME}/cmdline-tools && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip && \
    unzip commandlinetools-linux-*.zip && \
    mv cmdline-tools latest && \
    mkdir -p ${ANDROID_HOME}/licenses && \
    echo "24333f8a63b6825ea9c5514f83c2829b004d1fee" > ${ANDROID_HOME}/licenses/android-sdk-license

# Установка Android платформы и инструментов
RUN yes | sdkmanager --install "platforms;android-33" "build-tools;33.0.0" "platform-tools"

# Настройка Flutter
RUN flutter doctor --android-licenses --verbose > /dev/null 2>&1 || true
RUN flutter precache
RUN flutter doctor
