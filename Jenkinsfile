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
                git branch: "${GIT_BRANCH}", credentialsId: '67191338-eb19-4778-90be-4d9335c6f5d5', url: 'https://github.com/leonidfrolov/spring-petclinic'
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
                                "pattern": "target/**.jar",
                                "target": "test/com/epam_labs/frolov/"
                            }
                        ]
                    }'''
                )
            }
        }
    }
}
