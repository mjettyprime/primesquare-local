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
        // stage('clone') {
        //     steps {
        //         // Get some code from a GitHub repository
        //         git credentialsId: 'Git-hub', url: "${Repo}"
        //     }
        // }    
        stage('Build') {
            steps {
                sh "mvn clean install"
            }    
        }        
    }
}
