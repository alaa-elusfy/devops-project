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
		sh "docker build -t alaaelusfy/train-application:1.0 ."
            }
        }
        stage('PUSH_IMAGE') {
            steps {
                echo 'STAGE: PUSH_IMAGE'
		withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
			sh "docker login -u ${USER} -p ${PASSWORD}"
			sh "docker push alaaelusfy/train-application:1.0"
    		}
            }
        }
    }
}

