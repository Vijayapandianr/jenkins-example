
import groovy.io.FileType
 
pipeline {
    agent any
    
    stages {
        stage('Checkout Stage') {
            steps {
			checkout scm
            }
        }
	    stage('File path') {
		    steps{
			    script {
				    //def changeLogSets = currentBuild.changeSets
				    def fpath = filepath()
				    print fpath
			    }
		    }
	    }
	    
	    
        stage('Analysis and Unit Test stage') {
            parallel {
		stage('Unit Testing') {
			when {
                branch 'feature/*'
            }
            steps {
				echo 'feature'
			}
		}

		     stage ('File Counting') {

            steps {
		    script{
			        
                    currentBuild.rawBuild.getChangeSets().each { cs ->
                      cs.getItems().each { item ->
                        item.getAffectedFiles().each { f ->
                          println f
                        }
                      }
                    }
                }
            }
        }
        

		        stage('Sonar scan') {
			when {
				anyOf {
					branch 'PR-*'; branch 'feature/*'
				}
            }
            steps {
                    echo 'Sonar'
            }
        }
            }
        }
	
        stage('Unit Test Results') {
           	when {
                branch 'feature/*'
            }
            steps {
                echo 'Unit'
            }
        }


        stage('Sonar quality') {
			when {
				anyOf {
					branch 'PR-*'; branch 'feature/*'
				}
            }
            steps {
					echo 'quality'
            }
        }
      
        stage('Pull request decision stage') {
			when {
                branch 'PR-*'
            }
            steps {
                script {
                env.BooleanParam = input(message: 'Do you like to deploy?', ok: 'Yes', 
                                parameters: [booleanParam(defaultValue: false, 
                                description: 'If you like to Deploy, just push the button',name: 'Yes?')])
        
                }
            }  
        }
	//parallel branching loop
        stage('Decide the deployment environment') {
            when {
                expression { "${env.BooleanParam}" == 'true' }
            }	
            steps {
                script {
                    env.Env_Value = input message: 'User input required', ok: 'Submit',
                            parameters: [choice(name: 'Env_Value', choices: 'UAT\nPROD\nEXIT', description: 'Please select the environment to deploy')]
                }
            } 
        }
		
        stage('Deploy to EnviroServers') {		
            parallel {
		stage('Deploy to UAT') {
            when {
                expression { "${env.Env_Value}" == 'UAT' && "${env.Env_Value}" != 'EXIT'}
            }
            steps {
				echo 'Deployed to UAT'
			}
		}

		stage('Deploy to Prod') {
            when {
                expression { "${env.Env_Value}" == 'PROD' && "${env.Env_Value}" != 'EXIT'}
            }
            steps {
                    echo 'Deployed to PROD'
            }
        }
		stage('Deploy to Release') {
			when {
                branch 'release/*'
            }
	        steps {
              input message: 'Are you sure to deploy to release? (Click "Proceed" to continue)'
					echo 'Release'
            }
        }
            }
        }
  
		stage('Tosca Testing') {
			when {
                anyOf {
					branch 'PR-*'; branch 'release/*'
				}
            }
            steps {
					echo 'Tosca'
            }
        }
    }

     
    
}

def filepath () {
	
def changeLogSets = currentBuild.changeSets
	for (int i = 0; i < changeLogSets.size(); i++) {
    def entries = changeLogSets[i].items
    for (int j = 0; j < entries.length; j++) {
        def entry = entries[j]
        echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
        def files = new ArrayList(entry.affectedFiles)
        for (int k = 0; k < files.size(); k++) {
            def file = files[k]
            echo "  ${file.editType.name} ${file.path}"
        }
    }
}
}
