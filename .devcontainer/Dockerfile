FROM debian:bullseye

# Install dependencies
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa clang cmake ninja-build pkg-config libgtk-3-dev openjdk-11-jdk \
    && apt-get clean

# Install Flutter SDK
RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter -b stable
ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Install Android SDK
ENV ANDROID_SDK_ROOT="/usr/local/android-sdk"
RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools \
    && curl -o commandlinetools.zip https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip \
    && unzip commandlinetools.zip -d $ANDROID_SDK_ROOT/cmdline-tools \
    && rm commandlinetools.zip \
    && mv $ANDROID_SDK_ROOT/cmdline-tools/cmdline-tools $ANDROID_SDK_ROOT/cmdline-tools/latest

# Add Android SDK to PATH
ENV PATH="${PATH}:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools:${ANDROID_SDK_ROOT}/emulator"

# Accept licenses and install build tools + platform
RUN yes | sdkmanager --licenses
RUN sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2"

# Pre-download Flutter dependencies
RUN flutter doctor
