node ('Linux') {

		stage ('Build') {
			//adding a comment for the commit test
			env.DEPLOY_CREDS = credentials('deploy-anypoint-user')
			env.MULE_VERSION = '4.1.4'
			env.BG = "CIS"
			env.WORKER = "Micro"
			sh 'mvn -B -U -e -V clean -DskipTests package'
		}
		stage ('Test') {
			sh 'mvn test'
		}
		
		stage ('Deploy Production') {
			environment 
				ENVIRONMENT = 'Production'
				APP_NAME = 'DevOps_Demo_Hello_World'
			
			sh 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'
		}
 // tools {
 //   maven 'Maven_3.6.3'
 // }

}