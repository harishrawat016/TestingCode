pipeline {
    //agent any
    
    agent {
		docker {
		 image 'test:latest'
			label 'docker'
			registryUrl 'https://453793953964.dkr.ecr.ap-south-1.amazonaws.com'
			args '-u root'
		}
	}
    environment {
	    AWS_ACCESS_KEY_ID = credentials('aws_access_key')
	    AWS_SECRET_ACCESS_KEY = credentials('aws_secret_key')

	}
    stages {
       
    stage('AWS Profile Set'){
        steps{
            sh '''
        aws configure set aws_access_key_id ${AWS_ACCESS_KEY_ID}
        aws configure set aws_secret_access_key ${AWS_SECRET_ACCESS_KEY}
        '''
        }
    }
    
    stage('Testing AWS Credentails'){
        steps{
            sh '''
                aws s3 ls
                tflint --version
                tfsec --version
                cat /etc/os-release
            '''
            
        }
    } 
    }
}
