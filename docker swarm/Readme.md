## Install Docker CE on all three nodes.

On all three servers, install Docker CE.

``` sudo apt-get update ```
``` sudo apt-get -y install apt-transport-https ca-certificates curl gnupg-agent software-properties-common ```
``` curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - ```
``` sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" ```
``` sudo apt-get update ```
``` sudo apt-get install -y docker-ce=5:18.09.5~3-0~ubuntu-bionic docker-ce-cli=5:18.09.5~3-0~ubuntu-bionic containerd.io ```

Add cloud_user to the Docker group so that you can run docker commands as cloud_user.
``` sudo usermod -a -G docker cloud_user ```
Log out each server, then log back in.

You can verify the installation on each server like so:
``` docker version ```

## Configure the swarm manager.
On the swarm manager server, initialize the swarm. Be sure to replace <swarm manager private IP> in this command with the actual Private IP of the swarm manager (NOT the public IP).
``` docker swarm init --advertise-addr <swarm manager private IP>; ```

## Join the worker nodes to the cluster.
On the swarm manager, get a join command with a token:
``` docker swarm join-token worker ```
This should provide a command that begins docker swarm join .... Copy that command and run it on both worker servers.

Go back to the swarm manager and list the nodes.
``` docker node ls ```
Verify that you can see all three servers listed (including the manager). All three should have a status of READY. Once all three servers are ready, you have built your own Docker swarm cluster!
