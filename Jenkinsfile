pipeline {
        agent { label "${LABEL_NAME}" }

    environment {
        IMAGE_NAME = "simpleimage"
        IMAGE_TAG = "${BUILD_NUMBER}"
        DOCKER_IMAGE = "${IMAGE_NAME}:${IMAGE_TAG}"
    }

    stages {

        stage('code') {
            steps {
                echo "cloning repo"
                git url: "https://github.com/Qazaidi123/agentrepo.git", branch: "main"
            }
        }

        stage('Build docker image') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Deploy Container') {
            steps {
                echo "stop existing container if it exist"
                sh "docker stop C3 || true"
                sh "docker rm C3 || true"
                echo "Starting new Container"
                sh "docker run -d -p 80:80 --name C3 ${DOCKER_IMAGE} tail -f /dev/null"
            }
        }
    }

    post {
        always {
            echo "pipeline finished"
        }

        success {
            emailext(
                subject: "SUCCESS: ${JOB_NAME}#${BUILD_NUMBER}",
                to: 'zaidi.qumar@gmail.com',
                body: "Build Success: ${BUILD_URL}"
            )
        }

        failure {
            emailext(
                subject: "FAILED: ${JOB_NAME}#${BUILD_NUMBER}",
                to: 'zaidi.qumar@gmail.com',
                body: "Build Failed: ${BUILD_URL}"
            )
        }
    }
}
