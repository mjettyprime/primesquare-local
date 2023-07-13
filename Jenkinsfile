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

stage('Uploading to JFrog Artifactory') {
                        steps{
                        rtUpload(
                        serverId: "Jfrog",
                        spec: '''{
                        "files":[{
                        "pattern": "module-a/target/*.jar",
                        "target": "http://172.16.5.121:8082/ui/admin/repositories/local/Test-repo"
                        }]
                        }
                        ''',
                        )
                        }
                }
                stage('Archieving the Artifact'){
                steps{
                archiveArtifacts artifacts: 'module-a/target/*.jar', followSymlinks: false
                }
                }
    }
}
           
