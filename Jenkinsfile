pipeline{
    agent any
    satges {
        stage('fetching git repo details')
        {
            steps{
            echo 'fetching git repo'
            git branch: 'springboot', url: "https://github.com/bharath-b-1312/Unisys_DevSecOps.git"
            sh 'ls'
        }
        }
           // creating second stage for docker build and test
         stage('docker build and test'){

         }  
    }
}