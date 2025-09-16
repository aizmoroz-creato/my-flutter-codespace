FROM mcr.microsoft.com/devcontainers/base:jammy

# Установка git (нужен для flutter create и pub get)
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Установка Flutter
ENV FLUTTER_HOME=/opt/flutter
ENV PATH=${FLUTTER_HOME}/bin:${PATH}

RUN git clone https://github.com/flutter/flutter.git -b stable ${FLUTTER_HOME}
RUN flutter precache

# Проверка установки
RUN flutter --version
