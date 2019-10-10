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
                git branch: 'dev', changelog: false, credentialsId: '67191338-eb19-4778-90be-4d9335c6f5d5', poll: false, url: 'https://github.com/leonidfrolov/spring-petclinic'
            }
        }
        stage('Test') {
            steps {
            sh 'cd ./spring-petclinic; mvn clean test'
            }
            tools {
                maven 'maven'
            }
        }
        stage('Build') {
            steps {
            sh 'cd ./spring-petclinic; mvn package -Dmaven.test.skip=true'
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
