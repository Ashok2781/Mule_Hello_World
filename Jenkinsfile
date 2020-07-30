pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.1.4'
    BG = "CIS"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            sh label: '', script: 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          sh label: '', script: 'mvn test'
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Design'
        APP_NAME = 'sandbox-omni-channel-api-Dev'
      }
      steps {
			sh label: '', script: 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'
      }
    }
    stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = 'prod-omni-channel-api-Prod'
      }
      steps {
            sh label: '', script: 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'
      }
    }
  }

  tools {
    maven 'Maven_3.6.3'
  }
}