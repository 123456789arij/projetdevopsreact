pipeline {
    agent none
    environment {
		DOCKERHUB_CREDENTIALS=credentials('arijabid')
	}
    stages {
        stage('Init') {
            agent any
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
        stage('Build nest') {
            agent any
            
            steps {
                dir('nest'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/nest:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/nest:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/nest:$BUILD_ID'
                }
            }
        }
        stage('Build react') {
            agent any
          
            steps {
                dir('react'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/react:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/react:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/react:$BUILD_ID'
                }
            }
        }
        stage('Cleanup'){
            agent any
            steps{
                sh 'docker logout'
            }
        }
    }
}
