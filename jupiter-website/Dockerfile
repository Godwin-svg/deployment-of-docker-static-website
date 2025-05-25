FROM amazonlinux:latest

# Update package manager and install dependencies
RUN  yum update -y && \
     yum install -y  wget  httpd unzip

# Create a working directory
WORKDIR /var/www/html

# download websites
RUN wget https://github.com/Godwin-svg/Docker-static-app-file/raw/main/techmax-main.zip && \
    unzip techmax-main.zip && \
    cp -r  techmax-main/. /var/www/html && \
    rm -rf techmax-main techmax-main.zip

# Expose port 80 on the container
EXPOSE 80

# set default command that will start when tyhe container start
ENTRYPOINT [ "/usr/sbin/httpd", "-D", "FOREGROUND" ]

