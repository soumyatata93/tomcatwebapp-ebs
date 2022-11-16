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
                        sh 'mvn clean package'
                    }
                }

                stage ("Deployment"){
                    steps {
                        sh 'echo "Deployment...."'
                    }
                }
            }
        }
    }
}
