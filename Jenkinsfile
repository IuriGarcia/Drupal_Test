pipeline {
	    agent any

	        // Environment Variables
	        environment {
	        HOST = credentials('HOST')
            USER = credentials('USER')
            PSW = credentials('PSW')
	    }
	

	    stages {
            
	        stage('Remote SSH PUT'){
                script {    
                    def remote = [:]
                    remote.name = 'Rhel Dev'
                    remote.host = "${env.HOST}"
                    remote.user = "${env.USER}"
                    remote.password = "${env.PSW}"
                    remote.allowAnyHosts = true
                }
                writeFile file: 'abc.sh', text: 'ls -lrt'
                sshPut remote: remote, from: 'abc.sh', into: '.'                      
	        }

	    }
	

	    // Options
	    options {
	        // Timeout for pipeline
	        timeout(time:80, unit:'MINUTES')
	        skipDefaultCheckout()
	    }	

	    // 
	    post {
	        success {
	            echo 'Deployment has been completed!'
	        }
	        failure {
	          echo "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.JOB_DISPLAY_URL})"
	        }

	    }
	

	}