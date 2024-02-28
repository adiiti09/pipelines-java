pipeline {
    agent any

    stages {
         
        stage('Checkout') {
            
            steps {
                // Get some code from a GitHub repository
                git branch: 'main',
                    url: 'https://gitlab.com/nravinuthala/pipelines-java.git'

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
        stage ('Deploy') {

        steps {
            echo "deploy stage"
            deploy adapters: [tomcat9 (
                    credentialsId: 'tomcat_aditi',
                    path: '',
                    url: 'http://13.91.97.254:8081/'
                )],
                contextPath: 'test',
                onFailure: 'false',
                war: '**/*.war'
        }
    }

    }
}
