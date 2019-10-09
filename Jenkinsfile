pipeline {
    agent any
    stages {
        stage('clean') {
            steps {
                cleanWs()            
            }
        }
        stage('Clone') {
            steps {
                sh 'git clone https://github.com/leonidfrolov/spring-petclinic'
            }
            tools {
                git 'Default'
            }
        }
        stage('Test') {
            steps {
            sh 'cd /var/lib/jenkins/workspace/Job_F/spring-petclinic; mvn clean test'
            }
            tools {
                maven 'maven'
            }
        }
        stage('Build') {
            steps {
            sh 'cd /var/lib/jenkins/workspace/Job_F/spring-petclinic; mvn package'
            }
            tools {
                maven 'maven'
            }
        }
        stage('Deploy') {
            steps {
                rtUpload (
                    serverId: 'artifactory',
                    spec: '''{
                        "files": [
                            {
                                "pattern": "spring-petclinic/target/**.jar",
                                "target": "test/com/epam_labs/frolov/"
                            }
                        ]
                    }'''
                )
            }
        }
    }
}