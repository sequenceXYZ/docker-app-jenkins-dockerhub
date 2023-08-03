pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    stage('gitclone') {
                steps {
		    git 'https://github.com/sequenceXYZ/docker-app-jenkins-dockerhub'
		}
            }
	    stage('Build') {
	        steps {
	            sh 'docker build -t sequencexyz/centos_test:latest .'
		}
	    }
            stage('Login') {
	        steps {
		    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
		}
	    }
	    stage('Push') {
                steps {
	    	    sh 'docker push sequencexyz/centos_test:latest'
		}
	    }
	}

	post {
	    always {
	        sh 'docker logout'
	    }
	}
   }
