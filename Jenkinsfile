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
        stage("deployToTomcat") {
            steps {
                script {
                    def serverUrl = 'http://15.229.35.169:8080' // Change to your Tomcat server URL
                    def tomcatCredentialsId = 'tomcat' // Set your Tomcat credentials ID
                    def warFileName = "mass-2.2.war"
                    
                    // Download the artifact from Nexus
                    nexusArtifactDownloader(
                        artifacts: [
                            [
                                groupId: 'demo',
                                artifactId: 'mass',
                                version: '2.2',
                                classifier: '',
                                type: 'war',
                                target: "target/${warFileName}"
                            ]
                        ],
                        nexusVersion: 'nexus3',
                        nexusUrl: 'http://18.229.160.68:8081',
                        credentialsId: 'nexus'
                    )

                    // Deploy the downloaded artifact to Tomcat
                    tomcatDeploy(
                        credentialsId: tomcatCredentialsId,
                        url: serverUrl,
                        path: '/manager/class',
                        war: "target/${warFileName}",
                        version: "2.2"
                    )
                }
            }
        }
    }
}
