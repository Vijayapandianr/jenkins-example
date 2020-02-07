pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                echo "Compile staage"
                }
            }
        

        stage ('Testing Stage') {

            steps {
                 echo "Testting staage"
                }
            }
        


        stage ('Deployment Stage') {
            steps {
                echo "Deployment staage"
                }
            }
        }
    
 post { 
        always { 
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }

}
