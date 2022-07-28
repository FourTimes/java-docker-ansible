## java-docker-ansible

I'm going to describe how to build up this statck end end flow in this example. Here, I've chosen **Ubuntu** as the operating system.

Requirements

|SERVER| IP ADDRES|
|---|---|
| ubuntu | 192.168.0.10 |

_dependencies_

all the appliction are should running as a container. so you need to install the docker daemon and docker-compose  binary in your local machine. If your not installed in your execution machine please installit first. please follow below the instaructions.

If you are utilising a cloud virtual computer, take note. You must permit all port traffic. If you'd like to restrict access, we can do that later.

_docker installation commands_

```bash
echo -e "\e[1;31mdocker installation"
sudo apt-get update
sudo apt install curl git -y
sudo apt-get install ca-certificates curl gnupg lsb-release -y
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list >/dev/null
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
sudo systemctl start docker
sudo systemctl status docker
```

_docker compose installtion_

```bash
echo -e "\e[1;31mdocker-compose installation"
sudo curl -SL https://github.com/docker/compose/releases/download/v2.7.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose  version
```

Avoid permission issue you can switch the **root** user.

```bash
sudo -i
```

_copy the source repository to your virtual machine_

```bash
git clone https://github.com/FourTimes/java-docker-ansible.git
cd java-docker-ansible
```
sonar installation

```bash
sudo sysctl vm.max_map_count=262144
cd sonar
bash sonar-installation.sh
```

once execute the command you can validate the docker container status. It should be up and running.

```bash
sudo docker ps 
```

**Note** It should return, up and running status

_sonar login console_

open your browser with http://192.168.0.10:9000

_default credentials_

1. username is **admin**
2. password is **admin** 

it will request to change the default password.

![image](https://user-images.githubusercontent.com/91359308/181612050-6b8113fa-b00c-4181-9d0f-e4bf49370801.png)

![image](https://user-images.githubusercontent.com/91359308/181612251-1d7f9448-882b-4210-afce-a245d15c146d.png)




_jenkins installtion_

```bash
cd ..
cd jenkins
sudo bash bash.sh
```

once execute the command you can validate the docker container status. It should be up and running.

_jenkins console access_

open your browser with http://192.168.0.10:8080 Once load the jenkins web pages It should ask default password.

_how to find the jenkins default password_

```bash
sudo docker exec -ti jenkins_conatiner_name bash
cat 
```
