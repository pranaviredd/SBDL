pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'pipenv sync'
            }
        }

        stage('Test') {
            steps {
                bat 'pipenv run pytest'
            }
        }

        stage('Package') {
            when {
                anyOf {
                    branch "master"
                    branch "release"
                }
            }
            steps {
                powershell 'Compress-Archive -Path lib -DestinationPath sbdl.zip -Force'
            }
        }

        stage('Release') {
            when {
                branch 'release'
            }
            steps {
                echo 'Release stage completed - local Windows Jenkins'
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploy stage completed - local Windows Jenkins'
            }
        }
    }
}