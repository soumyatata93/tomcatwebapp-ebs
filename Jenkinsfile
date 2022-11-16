pipeline {
    agent any
    
     tools
    {
       maven "Maven"
    }
    




stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
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
                        deploy adapters: [tomcat7(credentialsId: 'TomcatID', path: '', url: 'http://3.110.104.177:8080')], contextPath: 'Redbus', war: '*/*.*'
                    }
                }
            }
        }
    }
}
