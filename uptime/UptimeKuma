# Use the official Ubuntu image as a base
FROM ubuntu:latest

# Install required packages and update the system
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y curl wget unzip tar zip git npm && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone the Uptime Kuma repository
RUN git clone https://github.com/louislam/uptime-kuma.git /opt/uptime-kuma

# Set working directory
WORKDIR /opt/uptime-kuma

# Install Uptime Kuma dependencies and set up the application
RUN npm run setup && \
    npm install pm2 -g && \
    pm2 install pm2-logrotate

# Expose the default port for Uptime Kuma
EXPOSE 3001

# Start Uptime Kuma using PM2
CMD ["pm2-runtime", "start", "server/server.js", "--name", "uptime-kuma"]
