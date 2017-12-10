properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		echo 'Unit Test Started'
		git 'https://github.com/moha5282/java-project.git'
		sh 'ant -f test.xml -v'   
		junit 'reports/result.xml'
		echo 'Unit Test Stage Completed'
	}   
	stage('Build') {    
		echo 'Build Stage Started'
		sh 'ant -f build.xml -v'   
		echo 'Build Stage Completed'
	}   
	stage('Deploy') {    
		echo 'Deploy Stage Started'
		sh 'aws s3 cp ${WORKSPACE}/dist/rectangle-$BUILD_NUMBER.jar s3://jenkins-s3bucket-fvdsbf2xcgcc' 
		echo 'Deploy Stage Completed'
	}
	stage('Report') {    
		echo 'Generating Report'
              withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'c40a1e61-b419-4b27-a237-4eef21ca23d8', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
			sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'    
}

                        }
	       echo 'Report Generation Successfull'

             }
