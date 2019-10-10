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
                sh 'printenv'
                git branch: "${GIT_BRANCH}", url: 'https://github.com/leonidfrolov/spring-petclinic'
            }
        }
        stage('Test') {
            steps {
            sh 'mvn clean test'
            }
            tools {
                maven 'maven'
            }
        }
        stage('Build') {
            steps {
            sh 'mvn package -Dmaven.test.skip=true'
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
                                "pattern": "$WORKSPACE/target/**.jar",
                                "target": "test/com/epam_labs/frolov/"
                            }
                        ]
                    }'''
                )
            }
        }
    }
}
