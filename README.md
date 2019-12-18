# Docker Compose Examples

This is a reference project that hopes to provide easy examples of Docker Compose files for ease of use. 

## CI/CD with Jenkins and SonarQube

Examples:
 - [jenkins_blueocean/docker-compose.yaml](./jenkins_blueocean/docker-compose.yaml)
 - [sonarqube_postgre_sql/docker-compose.yaml](./sonarqube_postgre_sql/docker-compose.yaml)

*nsure you have already installed Docker, DockerCompose, and Git*

How to use these files? Simply download the compose files into seperate folders, taking care to place them somewhere where you want data to persist (or adjust volumes correctly). Open a terminal  and navigate to the target directory and run:

```bash 
docker-compose up
```