pipeline {

    agent { label 'jenkins-bc-did' }

    stages {

        stage('Delete and deploy the service.') {
          steps {
            script {

                withCredentials([dockerCert(credentialsId: 'DOCKER_AUTH_CERTS', variable: 'DOCKER_CERT_PATH')]) {

                    sh "curl -X DELETE -H 'Content-Type: application/json' https://${SWARM_MANAGER_IP_AND_DOCKER_PORT}/services/registry --cert ${DOCKER_CERT_PATH}/cert.pem --key ${DOCKER_CERT_PATH}/key.pem  --cacert ${DOCKER_CERT_PATH}/ca.pem"

                    sh "sleep 20"

                    // Generate the secret text stored in jenkins with:
                    // echo "{\"username\":\"theusername\",\"password\":\"thepassword\",\"email\":\"theemail@server.com\",\"serveraddress\":\"docker.io\"}"  | base64 --wrap=0

                    sh "curl -X POST -H 'Content-Type: application/json' --data-binary '@deploy-swarm.json' https://${SWARM_MANAGER_IP_AND_DOCKER_PORT}/services/create --cert ${DOCKER_CERT_PATH}/cert.pem --key ${DOCKER_CERT_PATH}/key.pem  --cacert ${DOCKER_CERT_PATH}/ca.pem"
                }
            }
          }
        }
    }
}