pipeline {

    agent any
    tools {
        maven 'Maven 3.5.0' 
    }
    stages {
        stage('Compile stage') {
            steps {
                sh "mvn clean compile" 
        }
    }

        
  }

}
