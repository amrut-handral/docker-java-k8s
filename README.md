# docker-Java-kubernetes-project
Deploying Java Applications with Docker and Kubernetes

# Pre-req:
Java application
Docker
K8s cluster setup
Maven

# Project consists of basic microservice components with productcatalog, shopfront, and stockmanager.

# Deployment steps
1. Clone the Code from Git Repository
You start by downloading the project files to your local machine or server using Git.
Command:
git clone https://github.com/your-repo/project-name.git
This will create a local copy of the repository that contains the source code for all your microservices.

2. Build the Target Folder for Each Microservice Using Maven
Each microservice has a pom.xml file that defines its dependencies and build instructions. Use Maven to compile the code and create a JAR/WAR file in the target directory.
Command:
mvn clean install
clean deletes the previous build.
install compiles the code, runs tests, and packages it.
After this, you'll see a target/ directory with your deployable .jar file.

3. Build Docker Images for Each Microservice
Once the target directory exists and contains the compiled application, use Docker to create an image.
Command:
docker build -t your-dockerhub-account/imagename:tag .
Make sure the Dockerfile is present in the microservice’s directory.
The . indicates that Docker should look in the current directory for the Dockerfile.

4. Verify the Built Image
You can check if your image was successfully created using the docker images command.
Command:
docker images
Repeat Steps 2 to 4 for all other microservices to prepare their respective images.

5. Push the Docker Images to a Repository
If you’re working with a team or deploying to the cloud, pushing images to DockerHub or another registry makes them accessible to others.
Commands:
docker login
docker push your-dockerhub-account/imagename:tag

6. Reference the Images in Deployment Configuration Files
Your Kubernetes deployment YAML files (e.g., shopfront-service.yaml) will refer to the Docker image name and tag.
containers:
  - name: shopfront
    image: your-dockerhub-account/shopfront:tag
These YAML files tell Kubernetes how to deploy each microservice.

7. Deploy the Microservices to Kubernetes
Apply each YAML file to create the deployments and services.
Command:
kubectl apply -f shopfront-service.yaml
Repeat this for all other microservices

8. Verify Pod and Deployment Status
Ensure the pods are running and the deployment is successful.
Command:
kubectl get pods
kubectl get deployments
Look for status like Running and Ready.

9. Fetch the Service URL
Use kubectl to get the exposed service details, like IP and port.
Command:
kubectl get svc
If using a LoadBalancer, it will show an external IP. For NodePort, use the node IP and port shown.

10. Access the Application in the Browser
Open your browser and navigate to the service URL you retrieved.
Example: http://<external-ip>:<port> or http://localhost:<nodeport> depending on your setup.
