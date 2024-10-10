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
        // creating second stage for docker build and test
        
    }
}