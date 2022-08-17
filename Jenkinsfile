pipeline {
    agent any

    stages {
        stage("Initialize") {
            steps {
                cleanWs()
            }
        }
        stage('get SCM') {
            steps {
                git branch: 'develop', url: 'https://github.com/ofirbh91/jenkins.git'
                sh "cd ~/"
                sh "ls -l"
            }
        }
        stage('build'){
            steps{
                sh "docker build -t nodewebapp ."
                sh "docker images"
            }
        }
         stage('deploy'){
            steps{
                script{
                  try{
                    sh "docker kill nodewebapp"
                    sh "docker rm nodewebapp"
                    sh "docker run -itd --name nodewebapp -p 8081:3000 nodewebapp:latest &"
            }catch(e) {
                echo e.getMessage()
                sh "docker run -itd --name nodewebapp -p 8081:3000 nodewebapp:latest &"
            }
                }
            }
    }
    
}
    
}

