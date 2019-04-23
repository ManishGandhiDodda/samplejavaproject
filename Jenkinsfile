def workspace
node
{
    stage('checkout')
    {
        git 'git@github.com:ManishGandhiDodda/samplejavaproject.git'
        workspace = pwd()
    }
    stage('Build')
    {
        def mvnHome = tool name: 'M3', type: 'maven'
        withMaven(maven: 'M3', tempBinDir: '') {
        sh 'mvn clean install'
        }
    }
    stage('Code Analysis using Sonarqube')
    {
        workspace = pwd()
        def sonarHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        withSonarQubeEnv('SonarQube Server') {
            sh "${sonarHome}/bin/sonar-scanner"
            
        }
    }
    stage('Deploy onto Tomcat')
    {
        echo "Deployement stage"
        sh 'cp ./multi-module/webapp/target/*.war /usr/local/apache-tomcat-9.0.19/webapps'
     //   sh "find . -iname "*.war" -exec cp {} /usr/local/apache-tomcat-9.0.19/webapps \;"
    }
}
