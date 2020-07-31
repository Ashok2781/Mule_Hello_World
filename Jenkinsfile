node('Linux'){
    
    env.DEPLOY_CREDS = credentials('deploy-anypoint-user')
    env.MULE_VERSION = '4.1.4'
    env.BG = "CIS"
    env.WORKER = "Micro"
    env.ENVIRONMENT = 'Production'
    env.APP_NAME = 'prod-omni-channel-api-Prod'


//stage('Checkout') {
//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], //userRemoteConfigs: [[credentialsId: 'MuleRepogithub1', url: 'https://github.com/Ashok2781/Mule_Hello_World']]])
//}  

stage('Build') {
sh '''ls -ltr /opt/maven/bin'''
sh '''/opt/maven/bin/mvn --version'''
sh '''============================================================'''
sh '''pwd'''
sh '''ls -ltr'
sh '''============================================================'''
sh '''/opt/maven/bin/mvn -B -U -e -V clean -DskipTests package'''
sh '''============================================================'''

}

stage('Verify') {
sh '''/opt/maven/bin/mvn test'''
}

stage('Deploy-Prod') {
sh '''echo stage3 steps'''
sh '''echo $DEPLOY_CREDS'''
sh '''echo $MULE_VERSION'''
sh '''echo $BG'''
sh '''echo $WORKER'''
sh '''echo $ENVIRONMENT'''
sh '''echo $APP_NAME'''
sh '''/opt/maven/bin/mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'''
}

}