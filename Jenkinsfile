pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    stages {
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/RenoDeCortePXL/jgsu-spring-petclinic.git'
            }
        }
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "./mvnw clean package"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
