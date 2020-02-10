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
        
        
        stage ('File Counting') {

            steps {
                def tmpDirPath = "${env.workspace}//src"
                echo tmpDirPath
		         def tmpDir = new File(tmpDirPath)
                    tmpDir.eachFileRecurse(FileType.FILES) { file ->
                        echo "File: ${file}"
                    }
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
