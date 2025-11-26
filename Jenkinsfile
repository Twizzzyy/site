pipeline{
    agent any
        stages{
            stage("Take index"){
                steps{
                    git branch: "main",
                    url: "git@github.com:Twizzzyy/site.git"
                    credentialsId: "~/.ssh/id_ed25519_github"
                }    
            }
            stage("Show git directory"){
                steps{
                    sh '''
                        ls -la
                    '''
                }
            }
            stage("clone to nginx"){
                steps{
                    sshagent (credentials: ['~/.ssh/ed25519_deploy']){
                        rsync -avz index.html root@192.168.100.4:/var/www/html/index.html
                    }
                }
            }
        }
}
