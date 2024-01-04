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
        stage ("deploy-to-nexus") {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'mass',
                classifier: '',
                file: 'target/class.war',
                type: 'war']],
                credentialsId: 'nexus',
                groupId: 'demo',
                nexusUrl: '172.31.45.132:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'new-repo-store',
                version: '2.2'
            }
        }
    }
}
