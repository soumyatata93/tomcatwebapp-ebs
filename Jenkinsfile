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
                        deploy adapters: [tomcat7(credentialsId: 'TomcatID', path: '', url: 'http://13.233.11.166:8080/')], contextPath: 'RaviKiran', war: '*/*.*'
                    }
                }
            }
        }
    }
}
