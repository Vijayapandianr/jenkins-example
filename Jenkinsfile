pipeline {
    agent  {
         label 'sam_node'
    }
            
    stages {
        stage('Checkout') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Vijayapandianr/jenkins-example.git']]])
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
