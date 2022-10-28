pipeline {
    agent { label 'tuto' }
    
    enviroment{
        DOCKERHUB_CREDS = credentials('credential')
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    script {
                        sh 'podman build -t docker.io/khalilkan/web-go:$BUILD_NUMBER -f Dockerfile'
                    }
                }
                container('kubectl') {
                    script {
                        sh 'kubectl get pods'
                    }
                }
                container('fortune') {
                    script {
                        sh 'fortune'
                    }
                }
            }
        }
    }
}
