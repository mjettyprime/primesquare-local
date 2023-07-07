pipeline {
    agent {
        node {
            label "primesquare-local"
        }
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn"
    }

    stages {
        stage('Build') {
            steps {
                sh "mvn clean install"
            }    
        }        
    
		stage('Sonar'){
            steps{
                script {
					withSonarQubeEnv(credentialsId: 'sonar') {
					sh 'mvn sonar:sonar -Dsonar.projectName=test -Dsonar.projectKey=test'
					}
				}
			}
		}
		stage('Push artifacts into artifactory') {
            steps {
              rtUpload (
                serverId: 'my-artifactory',
                spec: '''{
                      "files": [
                        {
                          "pattern": "*.war",
                          "target": "example-repo-local/build-files/"
                        }
                    ]
                }'''
              )
			}
		}
			
		}
	}

