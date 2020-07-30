node('Linux'){
    
    env.DEPLOY_CREDS = credentials('deploy-anypoint-user')
    env.MULE_VERSION = '4.1.4'
    env.BG = "ed819f79-2ee4-43f7-928b-82325b50687a"
    env.WORKER = "Micro"
    env.ENVIRONMENT = 'Production'
    env.APP_NAME = 'prod-omni-channel-api-Prod'
    
//stage('Checkout') {
//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], //userRemoteConfigs: [[credentialsId: 'MuleRepogithub1', url: 'https://github.com/Ashok2781/Mule_Hello_World']]])
//}   
stage('Build') {
sh '''cd /opt'''
sh '''wget https://www-eu.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz'''
sh '''sudo tar xzf apache-maven-3.6.3-bin.tar.gz'''
sh '''sudo ln -s apache-maven-3.6.3 maven'''
sh '''sudo cat /etc/profile.d/maven.sh'''


//sh '''chmod -Rf 777 ./.mvn/wrapper'''
//sh '''chmod -Rf 777 ./mvnw'''
sh '''mvn --version'''
sh '''mvn -B -U -e -V clean -DskipTests package'''
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
sh '''mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'''
}

}