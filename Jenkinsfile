pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/John-Carlo-Brcelon/cicd.git'
        GIT_CREDENTIALS_ID = 'github-pat'
        GIT_BRANCH = 'main'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "*/${env.GIT_BRANCH}"]],
                    userRemoteConfigs: [[
                        url: "${env.GIT_REPO_URL}",
                        credentialsId: "${env.GIT_CREDENTIALS_ID}"
                    ]]
                ])
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                sudo rsync -av --delete \
                --exclude='venv/' \
                --exclude='.git/' \
                ./ /var/www/html/

                sudo chown -R www-data:www-data /var/www/html/
                '''
            }
        }

    }
}
