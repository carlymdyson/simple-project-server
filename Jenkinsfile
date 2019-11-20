pipeline {
    agent any
	environment {
 	   VERSION = readMavenPom().getVersion()
	}

    stages {
	stage ("version") {
		echo "${VERSION}"
	}

        stage('Test') {
            steps {
                    sh 'mvn test -Dtest=ControllerAndServiceSuite'
		    sh 'mvn test -Dtest=IntegrationSuite'
                }
            }
        stage('Build') {
            steps {
		sh 'mvn package -DskipTests'
                sh 'docker build -t="carlymdysondocker/simple-project-server:latest" .'
                }
            }
        stage('Deploy') {
            steps {
		sh 'docker push carlymdysondocker/simple-project-server:latest'
            }
        }

        stage('Testing Environment') {
            steps {
                echo "hello"
            }
        }
      stage('Staging') {
	when {
		expression {
			env.BRANCH_NAME == 'developer'
		}
	}
            steps {
                echo "staging"
            }
        }
      stage('Production') {
	when {
		expression {
			env.BRANCH_NAME == 'master'
		}
	}
            steps {
                echo "production"
            }
        }

    }

}


