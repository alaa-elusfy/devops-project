pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_PROJECT_KEY = 'train-project'
        SONAR_PROJECT_NAME = 'train-project'
    }

    stages {
        stage('PACKAGE') {
            steps {
                echo 'STAGE: PACKAGE'
		sh "mvn package"
            }
        }
        stage('TEST') {
            steps {
		script {
			withSonarQubeEnv("SonarQube") {
                        sh "mvn sonar:sonar -Dsonar.projectKey=${SONAR_PROJECT_KEY} -Dsonar.projectName=${SONAR_PROJECT_NAME}"
                    }
		}
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

