FROM jenkinsci/jnlp-slave:alpine

ENV HELM_VERSION v3.3.0
ENV HELM_FILENAME helm-${HELM_VERSION}-linux-amd64.tar.gz
ENV KUBE_LATEST_VERSION="v1.18.8"

USER root
WORKDIR /
RUN apk add --update -t deps curl tar gzip ca-certificates git
RUN curl -L https://get.helm.sh/${HELM_FILENAME} | tar zxv -C /tmp \
  && cp /tmp/linux-amd64/helm /usr/local/bin/helm \
  && chmod +x /usr/local/bin/helm

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
 && chmod +x /usr/local/bin/kubectl

RUN apk del --purge deps

RUN apk add --update mysql-client \
 && rm /var/cache/apk/*

USER jenkins
