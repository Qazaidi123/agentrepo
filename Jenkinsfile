pipeline {
    agent { label "${LABEL_NAME}" }
    envirornment {
        IMAGE_NAME = " simpleimage "
        IMAGE_TAG = "${BUILD_NUMBER}"
        DOCKER_IMAGE = "${IMAGE_NAME} : ${IMAGE_TAG}"
    }
    stages {
        stage ( 'code' ) {
            steps {
                git url:"https://github.com/Qazaidi123/agentrepo.git" , branch: "main"                 
            }
        }
        stage ( 'build' ) {
             steps {
                 sh "docker build -t ${DOCKER_IMAGE} ."
             }
        }   
        
         stage ('deploy') {
               steps {
                   sh "docker stop c2 || true"
                   sh "docker rm c2 || true"
                   sh "docker run -d -p 80:80 --name c2 ${DOCKER_IMAGE} sleep infinity"
                   
               }
    }
}
}
post {
    always {
        echo "pipeline finished"
    }
    success {
        emailext( subject: "SUCCESS: ${JOB_NAME}#${BUILD_NUMBER}", to: 'zaidi.qumar@gmail.com', body: "Build_Success: ${Build_URL}" )
    }
    failure {
        emailext( subject: "FAILED: ${JOB_NAME}#${BUILD_NUMBER}" , to: 'zaidi.qumar@gmail.com' , body: "Build _Failed: ${BUILD_URL}" )
    }
}
