node('Linux'){
    
    env.DEPLOY_CREDS = credentials('deploy-anypoint-user')
    env.MULE_VERSION = '4.1.4'
    env.BG = "ed819f79-2ee4-43f7-928b-82325b50687a"
    env.WORKER = "Micro"
    env.ENVIRONMENT = 'Production'
    env.APP_NAME = 'DevOps_Demo_pipeline'


stage('Checkout') {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'MuleRepogithub1', url: 'https://github.com/Ashok2781/Mule_Hello_World']]])
}  
stage('Build') {
sh '''/opt/maven/bin mvn --version'''
sh '''/opt/maven/bin/mvn -B -U -e -V clean -DskipTests package'''
}
stage('Verify') {
sh '''mvn test'''
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