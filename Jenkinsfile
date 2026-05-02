pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'repo link'
        GIT_CREDENTIALS_ID = 'aa2a2b28-5a07-4a83-b8f8-670c9867bc1e'
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
