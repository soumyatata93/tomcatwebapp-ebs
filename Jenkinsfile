pipeline {
    agent any
    
     tools
    {
       maven "Maven"
    }
    




stages{
        stage('Build'){
            steps {
                sh 'mvn package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('UnitTest'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh 'mvn clean test'
                    }
                }

                stage ("Deployment"){
                    steps {
                        deploy adapters: [tomcat9(credentialsId: 'tomcar', path: '', url: 'http://13.212.250.132:8080/')], contextPath: 'Redbus', war: '*/*.war'
                    }
                }
            }
        }
    }
}
