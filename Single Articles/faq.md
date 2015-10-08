Date:2015-10-05 13:40
Title: Some problems I met when using Docker
Author:Lotp
Tag:Docker
##Solution to the "client and server don't have same version (client: 1.14, server: 1.12)" error
* Install lower version of compose
* Install higher version of docker

##Trap about 'shared directory'
The first synchronization will always synchronize directory within container with the host one.

For example
In your docker-compose.yml, you have one line like this:

	volumes:
	        - ./src:/myApp

When your image is first started, /myApp within container with always be synchronized as ./src in your host.

Even if it has something different from ./src
