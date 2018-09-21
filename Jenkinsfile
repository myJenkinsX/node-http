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
                API_KEY = "DMiEBHiD3F5F2CrqwLJD9MPFEUJbbm_G5fa-firKEp87"
            }            
            steps{
                container('nodejs') {
                    //sh "apt-get update"
                    //sh "apt-get install -y sudo"
                    //sh "curl -sL https://ibm.biz/idt-installer | bash"
                    sh "curl -fsSL https://clis.ng.bluemix.net/install/linux | sh"
                    sh "ibmcloud login --apikey $API_KEY"                    
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
