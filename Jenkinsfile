pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/rajesh1274/DevSecOps.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    
    
    
    
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
    stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'sudo cp target/*.war /home/rajesh4debug/prod/apache-tomcat-8.5.42/webapps/webapp.war'
              }      
           }       
    }
    
    
    
    
  }
}
