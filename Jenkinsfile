pipeline {
    agent any
    tools {
        maven "maven"
    }
    stages {
        stage ("checkout") {
            steps {
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/Harshitha-Aishu/hashitha-demo.git'
            }
        }
        stage ("build") {
            steps {
                sh "mvn install"
            }
        }
    }
}