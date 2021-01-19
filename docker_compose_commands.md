Please remember to check your Docker version along with the file version if you run into any issues. You can find more here:

https://docs.docker.com/compose/compose-file/compose-versioning/


The following commands can be found at https://docs.docker.com/compose/reference/


A list of core commands includes the following:


### Docker-compose up

Builds, (re)creates, starts, and attaches to containers for a service.


### Docker-compose start

Starts existing containers for a service.


### Docker-compose stop

Stops running containers without removing them. They can be started again with docker-compose start.


### Docker-compose ps

This command will list containers


### Docker-compose down

Stops containers and removes containers, networks, volumes, and images created by up.



For a Compose file, we build a YML or YAML (.yml or .yaml both work) to define our services, networks, and volumes. The default path for a Compose file is ./docker-compose.yml.


For examples of version 3 please see: https://docs.docker.com/compose/compose-file/#compose-file-structure-and-examples


Docker Compose File Reference: https://docs.docker.com/compose/


Also, when building a compose file the following reference can be extremely helpful:

https://docs.docker.com/compose/compose-file/#expose

