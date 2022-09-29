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
                //}
                //changed {
                    emailext attachLog: true, 
                    body: "Please go to ${BUILD_URL} and verify the build", 
                    compressLog: true, 
                    recipientProviders: [upstreamDevelopers(), requestor()], 
                    subject: "Job \'${JOB_NAME}\' (build ${BUILD_NUMBER}) ${currentBuild.result}", 
                    to: 'renojkdc@hotmail.com'
                }
            }
        }
    }
}
