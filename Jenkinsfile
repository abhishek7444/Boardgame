pipeline {
    agent any
    tools {
        jdk "JDK"
        maven "maven"
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/abhishek7444/Boardgame.git'
            }
        }
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        stage('Trivy FS') {
            steps {
                sh "trivy fs . --format table -o fs.html"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarQubeServer') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=boardGame -Dsonar.projectKey=boardGame \
                          -Dsonar.java.binaries=target'''
                }
            }
        }
        stage('Build') {
            steps {
                sh "mvn package"
            }
        }
        stage('Publish Artifacts') {
            steps {
                withMaven(
                    maven: 'maven',                  
                    jdk: 'JDK',                      
                    mavenSettingsConfig: 'maven-settings'  
                 ) 
                 {
                    sh "mvn clean deploy"
                 }
            }
        }
        stage('Docker Build & Tag') {
            steps {
                script{
                withDockerRegistry(credentialsId: 'dockerhub-cred', url: 'https://index.docker.io/v1/') {
                sh "docker build -t abhishekjainse/boardgame ."
                }
                }
            }
        }
        stage('Trivy Image Scan') {
            steps {
                sh "trivy image --format table -o image.html abhishekjainse/boardgame:latest"
            }
        }
        stage('Docker Push Image') {
            steps {
                script{
                withDockerRegistry(credentialsId: 'dockerhub-cred', url: 'https://index.docker.io/v1/') {
                    sh "docker push abhishekjainse/boardgame"
                }
                }
            }
        }
        stage('K8s Deploy') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: ' boardGame-cluster', contextName: '', credentialsId: 'K8s-token', namespace: 'boardgame', serverUrl: 'https://4B4B55E0470DD5115542E75B005050C2.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yaml"
                    sleep 20
                }
            }
        }
        stage('Verify Deployment') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'boardGame-cluster', contextName: '', credentialsId: 'K8s-token', namespace: 'boardgame', serverUrl: 'https://4B4B55E0470DD5115542E75B005050C2.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl get pods -n boardgame"
                    sh "kubectl get service -n boardgame"
                }
            }
        }
    }  
}  
