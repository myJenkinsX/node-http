pipeline {
    agent {
        label "jenkins-nodejs"
    }
    environment {
      ORG               = 'wofish2'
      APP_NAME          = 'node-http'
      CHARTMUSEUM_CREDS = credentials('jenkins-x-chartmuseum')
    }
    stages {
        stage('Login IBM') {
            environment {
                API_KEY = "r4cDhWdpdjeueJVokgbZqdnEIbNyjvRGZV86SeIJKAtT"
                API_ENDPOINT = "https://api.au-syd.bluemix.net"
                REGISTRY_URL = "registry.au-syd.bluemix.net"
            }            
            steps{
                container('nodejs') {
                    
                    //sh "cat /home/jenkins/.docker/config.json"
   
                    sh "curl -fsSL https://clis.ng.bluemix.net/install/linux | sh"
                    sh "ibmcloud plugin install container-service"
                    sh "ibmcloud plugin install container-registry"
                    
                    sh "ibmcloud login --apikey $API_KEY -a $API_ENDPOINT"
                    sh "ibmcloud cs region-set ap-north"
                    sh "VAR3=\$(ibmcloud cs cluster-config mycluster --export) && \$VAR3"
                    //sh "ibmcloud cs cluster-get mycluster"
                    //sh "ibmcloud cr images"
                    
                    //sh "ibmcloud cr login"
                    sh "docker login -u DONGHAIY@jp.ibm.com -p $API_KEY $REGISTRY_URL"
                    sh "docker pull hello-world"
                    sh "docker tag hello-world:latest registry.au-syd.bluemix.net/wofish2/hello-world:2"
                    sh "docker push registry.au-syd.bluemix.net/wofish2/hello-world:2"
                    
                    sh "ibmcloud cr images"
                    //sh "ibmcloud cr images"
                    //sh "docker login -u iamapikey -p $API_KEY $REGISTRY_URL"                    
                    //sh "ibmcloud cr images"
                    
                }

            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
  }
