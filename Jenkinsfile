pipeline {
    agent any

    stages {
        stage('PACKAGE') {
            steps {
                echo 'STAGE: PACKAGE'
		sh "mvn package"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
