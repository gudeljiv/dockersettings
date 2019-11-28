#Borming Docker base server setup
This docker setup is used to simulate our server hosted @ Triton Grupa

#How to use
1. Install Docker - https://www.docker.com/
2. go to this folder and type : docker-compose up -d
3. Delete Vagrant :)

#How to add new websites
1. Edit vhosts file in ./config/vhosts/default.conf
2. Add new VirtualHost
3. docker-compose down
4. docker-compose up -d

#bin 
All custom docker images go here
- php:7.2-apache - Custom apache image, modify Apache2 - PHP here

#config
Used to map configuration files 
- php.ini
- vhosts for Apache2

#data
Used to map DB data files

#logs
Used to map log files 

#MYSQL
root password : borming
To connect from outside, use 127.0.0.1

#bye
05.08.2019 - Ozren