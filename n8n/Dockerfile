# Use an official n8n image as a parent image
# You can pin this to a specific version, e.g., n8nio/n8n:1.45.1
FROM n8nio/n8n:latest

# Switch to the root user to install system packages
USER root

# Install LibreOffice, FFmpeg, Python, and pip on Alpine
RUN apk update && \
    apk add --no-cache \
        libreoffice \
        libreoffice-writer \
        libreoffice-calc \
        libreoffice-impress \
        ttf-freefont \
        ffmpeg \
        python3 \
        py3-pip

# Install uv using pip, breaking system packages as this is a controlled environment
RUN pip3 install uv --break-system-packages

# Create a folder for temp files, and set permissions for node user
RUN mkdir /temp_files && chown node:node /temp_files && chmod 770 /temp_files

# Switch back to the non-root user that n8n runs as
USER node 