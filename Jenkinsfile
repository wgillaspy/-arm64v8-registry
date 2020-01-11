pipeline {

    agent { label 'jenkins-bc-did' }

    stages {

        stage('Delete and deploy the service.') {
          steps {
            script {
              sh "curl -X DELETE -H 'Content-Type: application/json' http://${SWARM_MANAGER_IP_AND_DOCKER_PORT}/services/registry"

              sh "sleep 20"

              // Generate the secret text stored in jenkins with:
              // echo "{\"username\":\"theusername\",\"password\":\"thepassword\",\"email\":\"theemail@server.com\",\"serveraddress\":\"docker.io\"}"  | base64 --wrap=0

              sh "curl -X POST -H 'Content-Type: application/json' --data-binary '@deploy-swarm.json' http://${SWARM_MANAGER_IP_AND_DOCKER_PORT}/services/create"
            }
            sh "sleep 120"
          }
        }
    }
}