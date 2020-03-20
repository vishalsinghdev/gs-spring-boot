node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp todo-app-java-on-azure-1.0-SNAPSHOT.jar app.jar 
         zip todo.zip app.jar web.config
      '''
   }
   stage('deploy') {
      azureWebAppPublish a8ccb851-f17a-4c80-8cdd-07400a5904ac: env.AZURE_CRED_ID,
      jenkins: env.RES_GROUP, vs1347jenkins: env.WEB_APP, filePath: "**/todo.zip"
   }
}