pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub_password')
	}

	stages {
	    stage('gitclone') {
                steps {
	            git branch: 'main', url: 'https://github.com/sequenceXYZ/docker-app-jenkins-dockerhub.git'
		}
            }
	    stage('Build') {
	        steps {
	            sh 'docker build -t sequencexyz/test-app:3 .'
		}
	    }
            stage('Login') {
	        steps {
		    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		}
	    }
	    stage('Push') {
                steps {
	    	    sh 'docker push sequencexyz/centos_test:3'
		}
	    }
	}

	post {
	    always {
	        sh 'docker logout'
	    }
	}
   }
