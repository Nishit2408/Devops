### Install Helm

Let's install `helm` in our container </br>

```
curl -L https://get.helm.sh/helm-v3.5.4-linux-amd64.tar.gz -o /tmp/helm.tar.gz && \
tar -xzf /tmp/helm.tar.gz -C /tmp && \
chmod +x /tmp/linux-amd64/helm && \
mv /tmp/linux-amd64/helm /usr/local/bin/helm

```