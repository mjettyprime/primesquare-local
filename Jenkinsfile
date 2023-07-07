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
		stage('Deploy to Environment') {
            steps {
                script {
                    def server = Artifactory.server('admin')
                    def deployer = server.newDeployer()

                    // Deploy artifacts from Artifactory to your environment
                    deployer.deploy(
                        pattern: 'module-a/target*.jar',
                        targetRepo: 'Test-repo'
                    )
                }
            }
        }
		stage('Archieving the Artifact'){
			steps{
			archiveArtifacts artifacts: 'module-a/target*.jar', followSymlinks: false
			}
		}		
			
		}
	}

