pipeline {
    agent any

    stages {
        stage('Take index') {
            steps {
                echo 'Клонируем репозиторий с GitHub'
                git branch: 'main',
                    url: 'git@github.com:Twizzzyy/site.git',
                    credentialsId: 'github2'    // <-- ID кредов из Jenkins
            }
        }

        stage('Show git directory') {
            steps {
                sh '''
                    pwd
                    ls -la
                '''
            }
        }

        stage('clone to nginx') {
            steps {
                sshagent (credentials: ['ssh-nginx']) { // <-- ID кредов для доступа к nginx
                    sh '''
                        rsync -avz -e "ssh -o StrictHostKeyChecking=no" index.html root@192.168.100.4:/var/www/html/index.html
                    '''
                }
            }
        }
    }
}
