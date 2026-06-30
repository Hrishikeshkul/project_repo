pipeline {
    agent {
        node {
            label 'built-in'
            customWorkspace '/mnt/war'
        }
    }

    stages {

        stage('SCM') {
            steps {
                sh '''
                    rm -rf *
                    git clone https://github.com/Hrishikeshkul/project_repo.git
                '''
            }
        }

        stage('Installing Docker') {
            steps {
                sh '''
                    yum install -y docker
                    systemctl start docker
                    systemctl enable docker
                    docker pull httpd
                '''
            }
        }

        stage('Creating index file inside container') {
            steps {
                sh '''
                    docker run -d -p 90:80 --name server1 httpd
                    docker cp /mnt/war/project_repo/index.html server1:/usr/local/apache2/htdocs/
                '''
            }
        }

    }
}
