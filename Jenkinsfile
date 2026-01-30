pipeline {
    agent { label "${LABEL_NAME}" }
    envirornment {
        IMAGE_NAME = " simpleapp "
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
                   sh "docker stop c1 || true"
                   sh "docker rm c1 || true"
                   sh "docker run -d -p 80:80 --name c1 ${DOCKER_IMAGE} sleep infinity"
                   
               }
    }
}
}
