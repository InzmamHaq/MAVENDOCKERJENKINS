pipeline {
    agent {
        node {
            label 'docker' && 'maven'
        }
    }
    stages {    
        stage('Build Jar') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                      // franautomation/containertest => organization/application - it could be anything
                      app = docker.build("franautomation/containertest")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    //docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${BUILD_NUMBER}")
                        app.push("latest")
                    //}
                }
            }
        }        
    }
}