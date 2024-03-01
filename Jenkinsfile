pipeline {
    agent any

    stages {
         
        stage('preparation') {
            
            steps {
                // Get some code from a GitHub repository
                git branch: 'master',
                    url: 'https://github.com/adiiti09/pipelines-java.git'

             }
        }

        stage ('Test') {

            steps {
                // Run Maven on a Unix agent.
                sh "mvn surefire-report:report"
                
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }

        stage ('Build') {

            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }
        stage ('Email config') {

        steps {
            mail bcc: '', body: 'Build success!', cc: '', from: '', replyTo: '', subject: 'Jenkins build status', to: 'aditianant2001@gmail.com'
        }
    }

    }
}
