pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                withMaven(maven: 'mvn'){
                    sh 'mvn -f pom.xml clean package'
                }
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