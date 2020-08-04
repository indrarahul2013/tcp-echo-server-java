pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3"
        dockerTool "docker"
    }

    stages {
        stage('VCS') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/indrarahul2013/tcp-echo-server-java'
            }
        }
        stage('Build') {
            steps {
                
                // Run Maven on a Unix agent.
                sh "mvn clean package"
            }
        }
        stage('Deploy') {
            steps {
                script {
                    withDockerRegistry(
                        credentialsId: 'b776e137-e3f0-41f2-beba-f3fe0cc5cb26',
                        toolName: 'docker') {
                        
                        // Build and Push
                        def echoServerImage = docker.build("indrarahul2018/java-echoserver:latest");
                        echoServerImage.push();
                    }
                }
            }
        }
    }
    post {
        success {
            echo "Success"
        }
        failure {
            echo "Fat Gya Bhai"
        }
    }
}
