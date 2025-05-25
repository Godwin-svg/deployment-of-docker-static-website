# Static Website Deployment with Docker and AWS ECS

This project demonstrates how to containerize a static website using Docker and deploy it on AWS ECS. The website is built into a Docker image, tested locally, 
pushed to Docker Hub and AWS ECR, and finally deployed in a secure, scalable AWS environment with a load balancer and domain configuration.

## Steps to Deploy the Static Website

1. Create a GitHub repository to store your Dockerfile and website files.  
2. Clone the GitHub repository to your local machine using:
  $ git clone <your-repo-url>
  $ cd <your-repo-folder>
3. Inside the project folder, create a Dockerfile with the following content:
4. Build the Docker container using the command:
  $  docker build -t jupiter .
5. Start and test the container locally using:
  docker run -d -p 8080:80 jupiter
  Then open your browser and go to http://localhost:8080 to confirm the website is working as expected.
6. Create a repository in your Docker Hub account to store the Docker image.
7. Push the image to Docker Hub:
  $ dockr login -u dockerhub_user_name
  $ enter password
  - Tag the image:
  $ docker tag jupiter your-dockerhub-username/image_name
  - Push the image:
  $ docker push your-dockerhub-username/image_name
8. Create an Amazon ECR repository to store your image using:
  $ aws ecr create-repository --repository-name repository_name --region us-east-1
9. Authenticate Docker to your Amazon ECR repository using:
  $ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.us-east-1.amazonaws.com
10. Tag the Docker image for ECR:
  $ docker tag jupiter <your-account-id>.dkr.ecr.us-east-1.amazonaws.com/repository_name
11. Push the image to the ECR repository:
  $ docker push <your-account-id>.dkr.ecr.us-east-1.amazonaws.com/repository_name
12. Build a three-tier VPC in AWS:
  - Public subnets (for Load Balancer)
  - Private subnets (for ECS containers)
13. Create security groups:
    - Application load balancer-SG : Allow inbound HTTP (port 80) and HTTPS (port 443) from the internet
    - Container-SG: Allow inbound traffic from ALB-SG only
14. Create a target group:
    - Choose IP addresses as the target type
15. Create an Application Load Balancer (ALB):
    - Associate it with public subnets and ALB-SG
16. In Route 53, create a DNS A record:
17. Use AWS Certificate Manager (ACM) to request or import an SSL certificate for your domain.
18. Create an HTTPS listener on the ALB, forward it to your target group, and attach the SSL certificate to secure your website







    



  
  
