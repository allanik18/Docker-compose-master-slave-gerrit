# Docker-compose-master-slave-gerrit

## Docker-compose configuration creates the following scenario:

1. Run image Jenkins master.
2. Run image Jenkins slave.
3. Run image Gerrit.
4. Jenkins master and Jenkins slave should be in the same docker network
5. Jenkins master and Gerrit should be in the same another docker network

## Requirements
1. Installed Docker-compose.
2. SSH key-pair in *ssh-keys* folder.
3. Jenkins configuration-as-code(plugin) config file in *master* folder. Find example *master/casc.yaml*
4. Desired plugins list in *master* folder. Example: *master/plugins.txt*
5. Jenkins pluggin **configuration-as-code:1.43**

## Usage

1. Run build images

```bash
$ docker-compose build
```
2. Run docker-compose 

```bash
$ docker-compose up
```
3. Services endpoints:
- Jenkins: http://localhost:8081
- Gerrit: http://localhost:8082
