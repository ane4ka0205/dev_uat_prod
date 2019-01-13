pipeline{
    agent any
    stages{
        stage("Pull repo"){
            steps{
                git 'https://github.com/ane4ka0205/dev_uat_prod.git'
            }
        }
        stage("Install requirements"){
            steps{
                sh "ssh root@104.248.56.181 yum install httpd -y" 
            }
        }
        stage("Move index.html"){
            steps{
                sh "scp ${workspace}/index.html root@104.248.56.181:/var/www/html/"
            }
        }
        stage("Start webserver"){
            steps{
                sh "ssh root@104.248.56.181 systemctl start httpd"
                sh "ssh root@104.248.56.181 systemctl enable httpd"
            }
        }
        stage("Ask input from user"){
            steps{
                input 'Would you like to proceed to UAT?'
            }
        }
        stage("Install requirements for UAT"){
            steps{
                sh "ssh root@68.183.26.92 yum install httpd -y" 
            }
        }
        stage("Move index.html for UAT"){
            steps{
                sh "scp ${workspace}/index.html root@68.183.26.92:/var/www/html/"
            }
        }
        stage("Start webserver for UAT"){
            steps{
                sh "ssh root@68.183.26.92 systemctl start httpd"
                sh "ssh root@68.183.26.92 systemctl enable httpd"
            }
        }
    }
}
