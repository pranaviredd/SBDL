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
               bat 'python -c "import shutil; shutil.make_archive(\'sbdl\', \'zip\', \'.\', \'lib\')"'
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
