FROM mcr.microsoft.com/devcontainers/java

# Rename default 'vscode' user (UID 1000) to 'palladio-devbox'
RUN usermod -l palladio-devbox -d /home/palladio-devbox -m vscode \
    && groupmod -n palladio-devbox vscode

# Install dependencies for Eclipse/Palladio
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
       libgtk-3-0 \
       libxtst6 \
       libglib2.0-0 \
       libfontconfig1 \
       libfreetype6 \
       libx11-6 \
       libxrender1 \
       libxext6 \
       libxi6 \
       wget \
       unzip \
    && rm -rf /var/lib/apt/lists/*

# Download and extract Palladio into /opt/palladio
RUN mkdir -p /opt/palladio \
    && wget -O /tmp/palladio.zip "https://updatesite.palladio-simulator.com/palladio-bench-product/releases/5.2.1/Palladio.linux.gtk.x86_64.zip" \
    && unzip /tmp/palladio.zip -d /opt/palladio \
    && rm /tmp/palladio.zip \
    && chown -R 1000:1000 /opt/palladio

# Create a dynamic wrapper script to launch Palladio silently. It also updates config.ini with $PWD before launching.
RUN echo '#!/bin/bash' > /usr/local/bin/palladio \
    && echo 'CONFIG_FILE="/opt/palladio/configuration/config.ini"' >> /usr/local/bin/palladio \
    && echo 'if [ -f "$CONFIG_FILE" ]; then' >> /usr/local/bin/palladio \
    && echo '    if grep -q "osgi.instance.area.default" "$CONFIG_FILE"; then' >> /usr/local/bin/palladio \
    && echo '        sed -i "s|osgi.instance.area.default=.*|osgi.instance.area.default=$PWD|" "$CONFIG_FILE"' >> /usr/local/bin/palladio \
    && echo '    else' >> /usr/local/bin/palladio \
    && echo '        echo "osgi.instance.area.default=$PWD" >> "$CONFIG_FILE"' >> /usr/local/bin/palladio \
    && echo '    fi' >> /usr/local/bin/palladio \
    && echo 'fi' >> /usr/local/bin/palladio \
    && echo 'nohup /opt/palladio/PalladioBench "$@" >/dev/null 2>&1 &' >> /usr/local/bin/palladio \
    && chmod +x /usr/local/bin/palladio

# Set working directory
WORKDIR /workspaces