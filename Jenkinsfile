pipeline {
    agent { label 'tuto' }
    
    environment{
        DOCKERHUB_CREDS = credentials('credential')
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    script {
                        sh 'podman build -t docker.io/khalilkan/web-go:$BUILD_NUMBER -f Dockerfile'
                        sh 'podman login docker.io -u $DOCKERHUB_CREDS_USR -p $DOCKERHUB_CREDS_PSW'
                        sh 'podman push docker.io/khalilkan/web-go:BUILD_NUMBER'
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
