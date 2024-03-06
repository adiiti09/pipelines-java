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
        stage ('Deploy') {

            steps {
                echo "deploy stage"
                deploy adapters: [tomcat9 (
                        credentialsId: 'tomcat_deploy_ui',
                        path: '',
                        url: 'http://20.62.99.46:8080/'
                    )],
                    contextPath: 'helloworld-app',
                    onFailure: 'false',
                    war: '**/*.war'
            }

    }

    }
}
