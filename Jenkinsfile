node
{
    def mavenHome = tool name: "maven-3.6.2"
    stage('Checkoutcode'){
        git branch: 'development', credentialsId: '84935e9e-ca78-44f5-bdf9-fea3844c6948', url: 'https://github.com/poreddysuriya/maven-web-application.git'
    }
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('Executesonarqubereport'){
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('Uploadartifacts'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('deployapptotomcat')
    sshagent(['bacde2eb-101d-4824-8830-9cf870bd8f35']) {
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.254.58:/opt/apache-tomcat-9.0.60/webapps"
    }
    stage('sendemailnotification'){
    mail bcc: 'poreddysomasekhar@gmail.com', body: 'Buildover', cc: 'poreddysomasekhar@gmail.com', from: '', replyTo: '', subject: 'Buildover', to: 'poreddysomasekhar@gmail.com'
    }
}
