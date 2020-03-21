## Docker Installation:
Install required packages:

sudo yum install -y device-mapper-persistent-data lvm2

Add the Docker CE repo:

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

Install the Docker CE packages and containerd.io:

sudo yum install -y docker-ce-18.09.5 docker-ce-cli-18.09.5 containerd.io

Start and enable the Docker service:

sudo systemctl start docker
sudo systemctl enable docker

Add cloud_user to the docker group, giving the user permission to run docker commands:

sudo usermod -a -G docker cloud_user

Log out and back in.

Test the installation by running a simple container:

docker run hello-world

## Selecting a Storage Driver:
Get the current storage driver:
docker info

Set the storage driver explicitly by providing a flag to the Docker daemon:
sudo vi /usr/lib/systemd/system/docker.service

Edit the ExecStart line, adding the --storage-driver devicemapper flag:
ExecStart=/usr/bin/dockerd --storage-driver devicemapper ...

After any edits to the unit file, reload Systemd and restart Docker:
sudo systemctl daemon-reload
sudo systemctl restart docker

We can also set the storage driver explicitly using the daemon configuration file. This is the method that Docker recommends. 
Note that we cannot do this and pass the --storage-driver flag to the daemon at the same time:

sudo vi /etc/docker/daemon.json

Set the storage driver in the daemon configuration file:
{
  "storage-driver": "devicemapper"
}

Restart Docker after editing the file. It is also a good idea to make sure Docker is running properly after changing the 
configuration file:

sudo systemctl restart docker
sudo systemctl status docker

## Configuring Logging Drivers (Splunk, Journald, etc.)

Check the current default logging driver:
docker info | grep Logging

Edit daemon.json to set a new default logging driver configuration:
sudo vi /etc/docker/daemon.json

Add the configuration to daemon.json:
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "15m"
  }
}

Restart docker after editing daemon.json:
sudo systemctl restart docker

Run a docker container, overriding the system default logging driver settings:
docker run --log-driver json-file --log-opt max-size=50m nginx

