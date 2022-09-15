@Library('pipeline-library-demo')_

def abc(String name = 'human') {
  echo "welcome to ${name} Program."
  echo "welcome to, ${name} practice."
}
node {
    def mvnHome
    
     stage("Ref lib"){
      abc "DevOps"
    }
    
    stage("shared lib"){
      sayHello "DevOps"
    }
    stage('Preparation') { 
       
        git 'https://github.com/jglick/simple-maven-project-with-tests.git'
        
        mvnHome = tool 'M3'
    }
    stage('Build') {
        
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
