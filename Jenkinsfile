pipeline {
    agent  {
         label 'sam_node'
    }
            
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
           mail to: 'vijayganesh6@gmail.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
            }
    }

}
