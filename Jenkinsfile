pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "Vimal"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/vimallearnz/cloudhub-deployment-vs.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'cloudhub-deployment-vs-cicd'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="vz-mule" -Danypoint.password="MWishes@01" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }
  }

  tools {
    maven 'M3'
  }
}
