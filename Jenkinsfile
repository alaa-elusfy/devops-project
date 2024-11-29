pipeline {
    agent any

    stages {
        stage('PACKAGE') {
            steps {
                echo 'STAGE: PACKAGE'
		sh "mvn package"
            }
        }
        stage('BUILD_IMAGE') {
            steps {
                echo 'STAGE: BUILD_IMAGE'
		sh "docker build -t train-project-img:1.0 ."
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
