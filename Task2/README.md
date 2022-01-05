The images created in Task 1 were tagged and uploaded to a public Docker Hub repository.

_Step1:_ Images were tagged prior to upload

docker tag api_frontend:latest giljaniz/api_frontend:v1
docker tag api_flask:latest giljaniz/api_flask:v1
docker tag api_nginx:latest giljaniz/api_nginx:v1

_Step2:_ Push Images to Repo
docker push giljaniz/api_nginx:v1
docker push giljaniz/api_flask:v1
docker push giljaniz/api_frontend:v1

_Step3:_ AWS Configuration
A T2.Micro EC2 Instance was created using the UBuntu 20.04 Base OS. Docker and Docker Compose were installed on the VM, and a security group was configured as follows:

- Allow Incoming on Port 80 from Anywhere
- Allow Incoming on Port 22 from Engineers' IP

An Elastic IP was created and associated to the above mentioned VM.

The stack was deployed using docker-compose

version: "3.7"

services:

        flask:
                image: giljaniz/api_flask:v1
                container_name: flask_app
                restart: always
                expose:
                     - 5000

        nginx:
                image: giljaniz/api_nginx:v1
                container_name: nginx-flask
                restart: always
                ports:
                        - "80:80"
                depends_on:
                        - "flask"

        frontend:
                image: giljaniz/api_frontend:v1
                container_name: react_frontend
                restart: always
                expose:
                    - 3000
                depends_on:
                    - "flask"
					
					
The App can be accessed over the Internet using the following URL: http://54.246.49.67/
