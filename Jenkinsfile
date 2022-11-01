pipeline {
    agent any
    tools { 
        maven 'Maven 3.6.0' 
        jdk 'jdk11' 
    }
    stages {
        stage('Initialize') {
            steps {
               echo "PATH = ${PATH}"
               echo "M2_HOME = ${M2_HOME}"
            }
        }
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }

    }
}