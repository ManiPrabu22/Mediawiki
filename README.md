Infra Overview
--------------
	- Two CentOS-7 VMs are deployed in Azure platform. One VM is configured as Master node and One VM is configured as worker node.
	- Private docker registry is configure in Master node where local images are pushed/pulled
	- Mariadb/Mysql is installed in Master node for application to use as a backend DB
	- Download the Mediawiki application and save in Master node
	- Build the docker image using DockerFile. This docker file will perform :
		-> Take apache:php image from docker hub 
		-> Install the php modules
		-> Copy the mediawiki folder to the apache:php image

Steps to deploy the application in infra
-----------------------------------------
1. Docker compose to build the docker image. #docker build -t <image-name>

2. Update the Deployment.yaml file with the image name and run the command #kubectl apply -f Deployment.yaml

3. Create the service by running  the command #kubectl apply -f  Service.yaml

4. Create the endpoints by running  the command #kubectl apply -f  Endpoint.yaml 

5. Now go to browser and access the URL http://<IP>:<<Node-port-no>/mediawiki and follow the instructions shown in the page.

Note : To autoscale the application based on the load , update the Deployment.yaml using below command
kubectl autoscale deployment <Deployment-name> --cpu-percent=<threshold-value> --min=<min-pods> --max=<max-pods>
