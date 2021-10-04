node
{
   def mavenHome = tool name: "Maven-3.6.2"
   stage('CheckoutCOde') {
   git branch: 'development', credentialsId: '0e45059e-8527-4c4c-8655-73aff1c341c5', url: 'https://github.com/poreddysuriya/maven-web-application.git'
   }
   stage('Build'){
   sh "${mavenHome}/bin/mvn clean package"
   }
   stage('ExecuteSonarQubeReport'){
   sh "${mavenHome}/bin/mvn clean sonar:sonar"
   }
   stage('UploadArtifactIntoNexusRepo'){
   sh "${mavenHome}/bin/mvn clean deploy"
   }
   stage('DeployTheapplicationIntoTomcatServer'){
   sshagent(['5eb83308-d889-4993-9770-03878060bfec']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.92.44:/opt/apache-tomcat-9.0.53/webapps"
   }
   }

   stage('sendEmailnotification'){
   mail bcc: 'frnds2suriya@gmail.com', body: '''Build Over!

   Regards,
   SOMA.''', cc: 'frnds2suriya@gmail.com', from: '', replyTo: '', subject: 'Build Over!', to: 'frnds2suriya@gmail.com'
   }  
}
