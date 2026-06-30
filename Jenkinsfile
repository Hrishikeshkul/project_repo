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
                    docker run -d -p 100:80 --name server4 httpd
                    docker cp /mnt/war/project_repo/index.html server4:/usr/local/apache2/htdocs/
                    docker exec -it server4 chmod 644 /usr/local/apache2/htdocs/index.html
                '''
            }
        }

    }
}
