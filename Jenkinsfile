pipeline {
    agent { label "${LABEL_NAME}" }
    stages {
        stage ( 'code' ) {
            steps {
                git url:"https://github.com/Qazaidi123/agentrepo.git" , branch: "main"                 
            }
        }
        stage ( 'build' ) {
             steps {
                 sh "docker build -t simpleapp:1 ."
             }
        }   
        
         stage ('deploy') {
               steps {
                   sh "docker stop c1 || true"
                   sh "docker rm c1 || true"
                   sh "docker run -d -p 80:80 --name c1 simpleapp:1 sleep infinity"
                   
               }
    }
}
}
