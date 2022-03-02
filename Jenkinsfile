pipeline {
    agent any
    stages {
        stage('submit stack') {
            steps {

	    sh "aws cloudformation create-stack --stack-name myCapstone.$(date +"%d%m%Y") --template-body file://simplests3cft.json --region 'us-west-2'"

	          }
		 }
		 }
		 }
