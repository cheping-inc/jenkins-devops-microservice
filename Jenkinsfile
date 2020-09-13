pipeline {
	agent any
	stages {
		stage('Build') {
			steps{
				echo "Build"
			}			
		}
		stage('Test') {
			steps{
				echo "Test"
				sh 'mvn --version'
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
			}
		}
	}
    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}
