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
                nexusArtifactUploader artifacts: [[artifactId: 'satish',
                classifier: '',
                file: 'target/tej.war',
                type: 'war']],
                credentialsId: 'nexus',
                groupId: 'demo',
                nexusUrl: '172.31.45.132',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'new-repo-store',
                version: '1.1.1'
            }
        }
    }
}
