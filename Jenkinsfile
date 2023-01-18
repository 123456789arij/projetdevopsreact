pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_nest')
    }
    stages {
         stage('Checkout'){
            agent any
            steps{
                //Changez avec votre lien github
                git branch: 'master', url: 'https://github.com/123456789arij/projetdevopsreact.git'
            }
        }
        stage('Init'){
            agent any
            steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Build nest') {
            agent any
            
            steps {
                dir('nest'){
                    sh 'docker build -t arijabid/nest:$BUILD_ID .'
                    sh 'docker push arijabid/nest:$BUILD_ID'
                    sh 'docker rmi arijabid/nest:$BUILD_ID'
                }
            }
        }
        stage('Build react') {
            agent any
          
            steps {
                dir('react'){
                    sh 'docker build -t arijabid/react:$BUILD_ID .'
                    sh 'docker push arijabid/react:$BUILD_ID'
                    sh 'docker rmi arijabid/react:$BUILD_ID'
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
