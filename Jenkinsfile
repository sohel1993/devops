node{
    def MavenHome = tool name : "Maven3.8.6"
    stage('CheckoutCode'){
        git branch: 'development', credentialsId: 'ab8ca329-7ab2-4e3d-90c3-86c35a12e323', url: 'https://github.com/sohel1993/maven-web-application.git'
    }
    stage('Build'){
        sh "${MavenHome}/bin/mvn clean package"
    }
    stage('CodeCheck'){
        sh "${MavenHome}/bin/mvn sonar:sonar"
    }
    stage('ArtifactRepo'){
         sh "${MavenHome}/bin/mvn deploy"
    }
    stage('TomcatServer'){
        sshagent(['bceaf9db-8929-4d6a-97b2-67f06dd5bde5']) {
     sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@15.206.169.225:/opt/tomcat9/webapps/"
}
    }
}
