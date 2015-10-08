Date:2015-10-06 23:20
Title:Serial 1:Seting Up the Development Environment with Docker
Author:Lotp
Tags:Docker, Ruby

## Prerequisite

Make sure you have installed docker and docker-compose.


An directory containing following files.


1. Gemfile
1. server.dockerfile
1. docker-compose.yml
1. An directory named which you should copy Gemfile to

The only thing you should change is the IP address in the docker-compose.yml.

##Building 
1. `docker-compose run server rail new .`(If asked overwrite, chose yes)
1. `docker-compose up.`

##Access Your ROR Site
1. Browse 'Your IP address:50004'(You should change the IP address to the one you
