pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Sonar scan') {
            steps {
                sh label: '', script: 'mvn clean package sonar:sonar'
            }
        }
        stage('Dependency check scan') {
            steps {
                sh label: '', script: 'mvn clean install'
            }
        }
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/ShruBR/DevOps-July-Batch.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean install"

            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.war'
                }
            }
        }
    }
}
