# Use an official n8n image as a parent image
# You can pin this to a specific version, e.g., n8nio/n8n:1.45.1
FROM n8nio/n8n:latest

# Switch to the root user to install system packages
USER root

# Update package lists and install Python, pip.
# Using -y to automatically say "yes" to prompts.
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    rm -rf /var/lib/apt/lists/*

# Install uv using pip
RUN pip3 install uv

# Switch back to the non-root user that n8n runs as
USER node 