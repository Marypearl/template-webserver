pipeline {
    agent any
    environment {
        SSH_CRED = credentials('webkey')
        def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@ec2-54-227-111-45.compute-1.amazonaws.com'
    }
    stages {
        
        stage('Build') {
            steps {
                echo 'building app'
                sh "ls"
                sh "pwd"
                sh "zip -r webapp.zip ."
                sh "ls"
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying'
                sshagent(['webkey']) {
                    sh 'scp -o StrictHostKeyChecking=no -i $SSH_CRED webapp.zip ubuntu@ec2-54-227-111-45.compute-1.amazonaws.com:/home/ubuntu'
                    
            }
        }


        stage('Clean-Up') {
            steps {
                echo 'Remove existing files'
            }
        }
    }
}
