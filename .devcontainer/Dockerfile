FROM debian:bullseye

# Install dependencies
RUN apt-get update && apt-get install -y \
    curl unzip git xz-utils zip libglu1-mesa clang cmake ninja-build pkg-config libgtk-3-dev \
    && apt-get clean

# Install Flutter SDK
RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter -b stable
ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

# Pre-download packages
RUN flutter doctor
