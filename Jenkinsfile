
Jenkinsfile

pipeline {
    agent any
    environment {
        PROJECT_ID = 'victormartinez1'
        CLUSTER_NAME = ' cluster-kubernet'
        LOCATION = 'us-central1-c'
        CREDENTIALS_ID = 'gke'
    }
    stages {
        stage("Checkout SCN") {
            steps {
                checkout scm
            }
        }
        stage('Build package') {
            steps {
                echo "Cleaning and packing"
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh 'mvn test'
            }
        }    
        stage('Build and push Docker Image') {
            steps {
                script {
                    appomage=docker.build( "victormartinez1/Andresdark2:${env.BUILD_ID}"}
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
       // stage('Deploy to GKE') {
         //   steps{
           //     sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
             //   step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            //}
        //}
    }    
}
