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
                    git clone -b dev https://github.com/Hrishikeshkul/project_repo.git
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
                    docker run -d -p 5050:80 --name server10 httpd
                    docker cp /mnt/war/project_repo/index.html server10:/usr/local/apache2/htdocs/
                    docker exec -it server10 chmod 644 /usr/local/apache2/htdocs/index.html
                '''
            }
        }

    }
}
