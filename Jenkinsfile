pipeline {
	agent any
	stages {
		stage('Build') {
			echo "Build"
			//sh 'mvn --version'
		}
		stage('Test') {
			echo "Test"
		}
		stage('Integration Test') {
			echo "Integration Test"
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
