pipeline {
    agent any
    tools {
	maven "MAVEN"
    }
    environment {
        // Set your Nexus credentials
        NEXUS_URL = 'https://127.0.0.1:8081/repository/maven-snapshots'
        NEXUS_CREDENTIALS_ID = 'nexus-cred'
    }
    stages {
        stage('PACKAGE') {
            steps {
                echo 'STAGE: PACKAGE'
		sh "mvn package"
            }
        }
        
	stage('DEPLOY') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${NEXUS_CREDENTIALS_ID}", usernameVariable: 'NEXUS_USERNAME', passwordVariable: 'NEXUS_PASSWORD')]) {
                        sh """
                            mvn deploy \
			    -s $HOME/.m2/settings.xml \
                            -DskipTests \
                            -DnexusUsername=${NEXUS_USERNAME} \
                            -DnexusPassword=${NEXUS_PASSWORD} \
                            -Dmaven.repo.local=$HOME/.m2/repository
                        """
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
