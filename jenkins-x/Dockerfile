FROM pmady7389/ubuntu:18.04

RUN apt-get update && apt-get install curl -y \
    && mkdir -p ~/.jx/bin \
    && curl -L "https://github.com/jenkins-x/jx/releases/download/$(curl --silent "https://github.com/jenkins-x/jx/releases/latest" | sed 's#.*tag/\(.*\)\".*#\1#')/jx-linux-amd64.tar.gz" | tar xzv "jx" \
    && mv jx /usr/local/bin
RUN jx --version
EXPOSE 8080

