pipeline {
    agent any
    environment {
        SSH_CRED = credentials('webkey')
        def CONNECT = 'ssh -o StrictHostKeyChecking=no ubuntu@54.227.111.45'
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
                echo 'Deploying app'
                sshagent(['webkey']) {
                    sh 'scp -o StrictHostKeyChecking=no -i $SSH_CRED webapp.zip ubuntu@54.227.111.45:/home/ubuntu'
                    sh '$CONNECT "sudo apt install zip -y"'
                    sh '$CONNECT "sudo rm -rf /var/www/html/"'
                    sh '$CONNECT "sudo mkdir /var/www/html/"'
                    sh '$CONNECT "sudo unzip webapp.zip -d /var/www/html/"'
                }
            }
        }


        stage('Clean-Up') {
            steps {
                echo 'Remove existing files'
                deleteDir()
            }
        }
    }
}
