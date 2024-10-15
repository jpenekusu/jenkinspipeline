pipeline {
    
    agent any

    tools {
        maven "M3"
    }

    stages {
        stage('Checking out the repo') {
            steps {
                checkout changelog: true, poll: true, scm: [$class: 'GitSCM', branches: [[name: '*/*']], 
                extensions: scm.extensions, userRemoteConfigs: [[credentialsId: 'github_token', url: 'https://github.com/jpenekusu/jenkinspipeline.git']]]
                sh "ls -lart ./"    
            }
        }
        stage('Compling ...') {
            steps {
                withMaven(maven:'M3') {
                    sh "mvn compile"
                }
            }
        }        
        stage('Testing ...') {
            steps {
                sh "mvn test"
            }
        }        
        stage('Building ...') {
            steps {
                sh "mvn -B -DskipTests clean package"
            }
        }

    }
}