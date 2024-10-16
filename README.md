# HMAPP

## installation du serveur de dev

### installation de nodejs

~~~bash

# installation de nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm --version
# installation de node
nvm install node
~~~

### installation de Docker

~~~bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Ajout de l'utilisateur courant au groupe docker
sudo usermod -aG docker $USER

~~~

## Application vuejs 3

~~~bash
npm create vuetify@latest my-vue-app

# > Recommanded
~~~