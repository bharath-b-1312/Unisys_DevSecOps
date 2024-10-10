pipeline {
    agent any
    stages {
        // create stage 1 for fetching git repo info
        stage('fetching git repo details'){
            // steps
            steps {
                echo 'fetching git repo'
                git branch: 'springboot', url:"https://github.com/bharath-b-1312/Unisys_DevSecOps.git"
                sh 'ls'
            }
            
        }
        // creating second stage for doing SAST analysis to identify critical vulnerability
        stage('SAST using trivy for critical vulns'){
            steps{
            echo 'using trivy to scan code pushed by developer'
            sh 'trivy fs --scanners vuln,secret,misconfig .'
            }
        }

        // using compsoe and curl 
        stage('compsoe for build ') {
            steps {
                echo 'running docker compose'
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
                sh 'docker-compose ps'
               
            }
            
        }

            // using docker pipeline to build and push 
        stage('building image and pushing it') {
            steps {
                echo 'using docker pipeline plugin to build and push image'
                script {
                    def imageName = "bharath1312/springboot"
                    def imageTag  = "tomcatdeploy$BUILD_NUMBER"
                    def bbCred = "27c08b75-0302-4ccb-a3d6-8c074d119785" //this we will get from jenkins page under ManageJenkins->Credentials
                    // building image 
                    docker.build(imageName + ":" + imageTag , " -f Dockerfile .")
                     //pushing image to dockerhub
                    docker.withRegistry('https://registry.hub.docker.com',bbCred){
                       docker.image(imageName + ":" + imageTag).push()
                  
                }
    
                }
            }
            
        }
        stage('checking connection with kubectl to AKS(azure kubernetes service)'){
            steps{
                echo 'getting kubectl version and nodes'
                sh 'kubectl get nodes'
                sh 'kubectl version'
            }

        }

        stage('deploying yaml files'){
            steps{
                echo 'using kubectl to deploy'
                sh 'kubectl apply -f deploy1.yaml -f service.yaml'
                sh 'kubectl get pods,service,deployment'
            }

        }

    }

}