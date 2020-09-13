pipeline {
	agent any
	//agent { docker{ image: 'maven:3.6.3' } }
	environment {
		dockerHome = tool 'MyDocker'
		mavenHome = tool 'MyMaven'
		PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD ID - $BUILD_ID"
				echo "TAG - $BUILD_TAG"
			}
		}
		stage('Compile') {
			steps{
				sh 'mvn clean compile'
			}
		}
		stage('Test') {
			steps{
				sh 'mvn test'
			}
		}
		stage('Integration Test') {
			steps{
				sh 'mvn failsafe:integration-test failsafe:verify'
			}
		}
		stage('Packaging') {
			steps{
				sh "mvn package -DskipTests"
			}
		}
		stage('Docker Build Image') {
			steps{
				script{
					dockerImage = docker.build("rodart/currency-exchange-devops:${env.BUILD_TAG}");
				}
			}
		}
		stage('Docker Push Image') {
			steps{
				script{
					docker.withRegistry('','MyDockerHub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
