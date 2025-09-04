# BoardgameListingWebApp

## Description

**Board Game Database Full-Stack Web Application.**
This web application displays lists of board games and their reviews. While anyone can view the board game lists and reviews, they are required to log in to add/ edit the board games and their reviews. The 'users' have the authority to add board games to the list and add reviews, and the 'managers' have the authority to edit/ delete the reviews on top of the authorities of users.  

## Technologies

- Java
- Spring Boot
- Amazon Web Services(AWS) EC2
- Thymeleaf
- Thymeleaf Fragments
- HTML5
- CSS
- JavaScript
- Spring MVC
- JDBC
- H2 Database Engine (In-memory)
- JUnit test framework
- Spring Security
- Twitter Bootstrap
- Maven

## Features

- Full-Stack Application
- UI components created with Thymeleaf and styled with Twitter Bootstrap
- Authentication and authorization using Spring Security
  - Authentication by allowing the users to authenticate with a username and password
  - Authorization by granting different permissions based on the roles (non-members, users, and managers)
- Different roles (non-members, users, and managers) with varying levels of permissions
  - Non-members only can see the boardgame lists and reviews
  - Users can add board games and write reviews
  - Managers can edit and delete the reviews
- Deployed the application on AWS EC2
- JUnit test framework for unit testing
- Spring MVC best practices to segregate views, controllers, and database packages
- JDBC for database connectivity and interaction
- CRUD (Create, Read, Update, Delete) operations for managing data in the database
- Schema.sql file to customize the schema and input initial data
- Thymeleaf Fragments to reduce redundancy of repeating HTML elements (head, footer, navigation)

## How to Run

1. Clone the repository
2. Open the project in your IDE of choice
3. Run the application
4. To use initial user data, use the following credentials.
  - username: bugs    |     password: bunny (user role)
  - username: daffy   |     password: duck  (manager role)
5. You can also sign-up as a new user and customize your role to play with the application! 😊


**
********************For Deployment:*********************

Tools Used:
Jenkins: For managing the CI/CD pipeline.
SonarQube: For static code analysis.
Nexus: For managing dependencies and artifacts.
Trivy: For scanning vulnerabilities in files and Docker images.
Docker: To containerize applications.
Prometheus: For monitoring metrics from services.
Grafana: For visualizing metrics.
Kubernetes (AWS EKS): For managing containerized workloads.


Step 1: Set up Git repository Security Token

Generated a personal access token for secure authentication with Git.

Step 2: Provisioned Servers

Deployed 3 EC2 instances on AWS:
Jenkins: t2.large, 25GB
SonarQube & Nexus: t2.medium, 20GB each
Enabled Auto-assign Public IP and configured security groups for SSH and required ports.

Step 3: Install Jenkins, SonarQube, and Nexus

Deploy Jenkins for managing the CI/CD pipeline.
Deploy SonarQube for static code analysis.
Deploy Nexus to manage build artifacts and dependencies.

Step 4: Configured Jenkins with Tools

Install necessary Jenkins plugins (Git, Docker, Kubernetes, SonarQube, Nexus).
Connect Jenkins to Nexus, Trivy, SonarQube, and DockerHub.
Configure credentials and integrations for seamless CI/CD execution.

Step 5: Created the CI/CD Pipeline

Define the Jenkins pipeline with stages:
Build
Test
SonarQube analysis
Artifact upload to Nexus
Docker image build and Trivy scan
Deployment to EKS

Step 6: Created EKS Cluster and Install CLI Tools

Provisioned AWS EKS cluster using the AWS console.
Installed AWS CLI and kubectl for cluster management.
Deployed Kubernetes manifests for the application via pipeline.

Step 7: Monitor the Application

Deployed Prometheus for collecting application and cluster metrics.
Configured Grafana dashboards for visual monitoring.

