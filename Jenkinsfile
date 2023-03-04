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
                        deploy adapters: [tomcat7(credentialsId: 'Tomcat', path: '', url: 'http://15.207.21.162:8080/')], contextPath: 'Redbus', war: '*/*.*'
                    }
                }
            }
        }
    }
}
