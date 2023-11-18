# docker-wordpress


![concepts](./assests/1681835937270.png)

## WordPress Application on Docker ,with phpMyAdmin,R53,Application Load Balancer & AWS Certificate Manager

### Why run Wordpress in Docker?
Running WordPress typically involves installing a LAMP (Linux, Apache, MySQL, and PHP) or LEMP (Linux, Nginx, MySQL, and PHP) stack, which can be time-consuming. However, by using tools like Docker and Docker Compose, you can streamline the process of setting up your preferred stack and installing WordPress

### Step 1: To launch an instance

Create your EC2 resources and launch your EC2 instance


![EC2 instance](./assests/1681839543180.png)

### Connect to instance via SSH client

![connect EC2 instance using SSH aws info ](./assests/Screenshot%202023-11-18%20131856.png)

##### Instance ID
 ``` i-025b81ada889226ff ``` (wordpress-docker)
1. Open an SSH client.
2. Locate your private key file. The key used to launch this instance is adp.pem
3. Run this command, if necessary, to ensure your key is not publicly viewable.
```
            chmod 400 adp.pem
```
4. Connect to your instance using its Public DNS:

```
            ec2-65-2-123-63.ap-south-1.compute.amazonaws.com
```

##### Example:
```
            ssh -i "adp.pem" ubuntu@ec2-65-2-123-63.ap-south-1.compute.amazonaws.com
```


### Step2: Connect to your Linux instance using SSH

![connect EC2 instance using SSH](./assests/Screenshot%202023-11-18%20132100.png)

I have added ssh **private key** (adp.pem) in assests directory

### Step 3: Check the OS Version
```
cat /etc/*release*
```

![Check the OS Version](./assests/Screenshot%202023-11-18%20140341.png)

### Step 4 : Install Docker Engine on Ubuntu with help of script file

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

![ Install Docker Engine on Ubuntu with help of script file](./assests/Screenshot%202023-11-18%20141103.png)

#####  NOTE "Please wait few minutes after run the script"

## check docker version

```
docker version
```

![docker version](./assests/Screenshot%202023-11-18%20141334.png)

## Step 5:  Install Docker Compose on Ubuntu 20.04

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```
![Install Docker Compose](./assests/Screenshot%202023-11-18%20141655.png)

## Check the docker compose version

```
docker-compose --version
```

![Check the docker compose version](./assests/Screenshot%202023-11-18%20141833.png)

## Step 6: Compose file build

```
git clone https://github.com/shabbiryahya/WordPress-Application-on-Docker.git
```

![git clone](./assests/Screenshot%202023-11-18%20143202.png)

```
 cd WordPress-Application-on-Docker
```

![directory content](./assests/Screenshot%202023-11-18%20143423.png)

Environment file -> .env_password

### build the docker images with help of docker-compose file

```
sudo docker-compose up --build -d
```

![build the docker images with help of docker-compose file](./assests/1681842279862.png)


### How to find Docker images

```
sudo docker images
```

![Docker images](./assests/Screenshot%202023-11-18%20145403.png)

### List of running docker container

```
sudo docker ps 
sudo docker-compose ps
```
![docker container](./assests/Screenshot%202023-11-18%20145631.png)

## Step 7 Connect to MySQL running in Docker container

```
sudo docker exec -it mysql_db_conatiner /bin/bash
```
![Connect to MySQL running in Docker container](./assests/Screenshot%202023-11-18%20145847.png)


```
 mysql -u root -p
```
![Connect to MySQL running in Docker container](./assests/Screenshot%202023-11-18%20150137.png)


#### Accessing a wordpress website container

```
sudo docker-compose ps
```
![Accessing a wordpress website container](./assests/1681843111988.png)

paste the public ip and port number  
public ip - http://52.66.124.163 
port number - 80  
http://52.66.124.163:80  


![Home Page](./assests/Screenshot%202023-11-18%20151047.png)

![Home Page](./assests/Screenshot%202023-11-18%20151235.png)

![Home Page](./assests/Screenshot%202023-11-18%20151437.png)

![Home Page](./assests/Screenshot%202023-11-18%20151537.png)

## Step 8: Check Wordpress application connected or not with MYSQL database

IP Address:Port number
http://52.66.124.163:8080

![phpMyAdmin Login Page](./assests/Screenshot%202023-11-18%20151819.png)

for credential goto ```.env_password``` -> ```# wordpress```


![phpMyAdmin Home Page](./assests/Screenshot%202023-11-18%20152107.png)

## Step 9: Create two target group


![Create two target group 1](./assests/1681846539940.png)

![Create two target group 2](./assests/1681846611520.png)

- everything is default and you will create first group & same second target group you will create only change port number and target group name  
- first target group name is docker-1 and port number is 80  
- second target group name is docker-2 and port number is 8080  

![Create two target group Home](./assests/1681847033031.png)

## Step10 : Create Application Load Balancer


![Create Application Load Balancer 1](./assests/1681847173042.png)
## select all subnet
![Create Application Load Balancer 2](./assests/1681847233644.png)

## select the docker-1 target group

![select the docker-1 target group 1](./assests/1681847337756.png)
![select the docker-1 target group 2](./assests/1681847393767.png)
![select the docker-1 target group 3](./assests/1681847459161.png)

















