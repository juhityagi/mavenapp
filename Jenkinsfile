
pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.8.6"
    }
    stages {
        stage('prep') {
            steps {
                git branch: 'main', url: 'https://github.com/juhityagi/mavenapp/'
            }
        }
        stage('build') {
            steps {
                
               sh 'mvn -f pom.xml -s settings.xml clean deploy'
                sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=maven \
  -Dsonar.host.url=http://34.73.137.145:9000 \
  -Dsonar.login=sqa_bb9d0c61f41e486b57ee9094751712e818a468b6'
     }
     
        post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
      }
    }

