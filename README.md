# Docker Compose Examples

This is a reference project that hopes to provide easy examples of Docker Compose files. 

## CI/CD with Jenkins and SonarQube

Examples:
 - [jenkins_blueocean/docker-compose.yml](./jenkins_blueocean/docker-compose.yml)
 - [sonarqube_postgre_sql/docker-compose.yml](./sonarqube_postgre_sql/docker-compose.yml)

*ensure you have already installed Docker, DockerCompose, and Git*

How to use these files? Simply download the compose files into seperate folders, taking care to place them somewhere where you want data to persist (or adjust volumes correctly). Open a terminal  and navigate to the target directory and run:

```bash 
docker-compose up
```

Windows example
```powershell
cd <drive>:\<git file directory>\jenkins_blueocean\
docker-compose up
```

Open another terminal

```powershell
cd <drive>:\<git file directory>\sonarqube_postgre_sql\
docker-compose up
```

### Connecting Jenkins to SonarQube, and SonarQube to Jenkins

Step #1 - Adding the plugin and updating the project files (assumes [Jenkins ver. 2.190.3](https://jenkins.io/changelog/) or later with Blueocean). Your new Jenkins server should be running at http://localhost:8080 unless you changed the [docker-compose.yml](./jenkins_blueocean/docker-compose.yml)

  - Open Jenkins administration 
  - Go to ```Manage>Configuration``` and scroll to ```SonarQube Servers``` section
  ![alt text](./docs/images/ManageJenkins.Configuration.SonarQube.JPG)
  - Click "Add SonarQube" button if the screen isn't showing the fields above
  - using "ipconfig" on Windows, or "ifconfig" on Linux, get your computers ("HOST") ip address and add it to the "**ServerURL**" field as shown: *http://host-ip:9000* where "**host-ip**" is your systems ip address

  - Now click "Advanced" button under "Server Authentication" token 
  ![alt text](./docs/images/ManageJenkins.Configuration.SonarQube.Advanced.jpg) You should see "Webhook Secret", we'll need to get the token from SonarQube to add here, open a new browser window to http://localhost:9000 

  Step #2 - Generating the Webhook Key from Sonar. Your new server should be at http://localhost:9000 unless you changed the [docker-compose.yml](./sonarqube_postgre_sql/docker-compose.yml)

  - Click the "Login" button, default user is "admin" and password is "admin" (you'll want to change this eventually)
  ![alt text](./docs/images/SonarQube.Login.JPG)

  - Once you've logged in, you should see a new "Administration" tab in the menu, click on that and then click "Configuration" to view the "Webhooks" menu item and click it ![alt text](./docs/images/SonarQube.Administration.Webhooks.JPG)


