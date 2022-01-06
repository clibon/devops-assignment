Since the output from Task1 consisted in dockerising the applications, the same images can be used on other Docker installations such as Cloud Infrastructure.

The images created in Task 1 were tagged and uploaded to a public Docker Hub repository.

_Step1:_ Images were tagged prior to upload from local dev machine to the public Docker Hub Repository.

docker tag api_frontend:latest giljaniz/api_frontend:v1
docker tag api_flask:latest giljaniz/api_flask:v1
docker tag api_nginx:latest giljaniz/api_nginx:v1

_Step2:_ Push Images to Repo
docker push giljaniz/api_nginx:v1
docker push giljaniz/api_flask:v1
docker push giljaniz/api_frontend:v1

_Step3:_ AWS Configuration

A t2.micro EC2 Instance was created using the Ubuntu 20.04 Base OS. Docker and Docker Compose were installed on the VM, and a security group was configured as follows:

- Allow Incoming Traffic on Port 80 (HTTP) from Anywhere
- Allow Incoming Traffic on Port 22 (SSH) from Engineer's IP

An public Elastic IP was created and associated to the above mentioned VM to allow for external connectivity to the application via the internet.

The stack was deployed using docker-compose syntax found within the attached docker-compose.yaml file.
					
The App can be accessed over the Internet using the following URL: http://54.246.49.67/
