pipeline {

    agent any
    tools {
        maven 'Maven 3.6.3' 
    }
    stages {
        stage('Compile stage') {
            steps {
                sh "mvn clean compile" 
        }
    }

        
  }

}
