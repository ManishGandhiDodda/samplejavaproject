def readpom;
node
{
    stage ('Codecheckout')
    {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '0becc3d3-39fd-4d03-9209-eec1722f0586', url: 'git@github.com:ManishGandhiDodda/samplejavaproject.git']]])
    }
    stage ('readPOM file')
    {
    readpom = readMavenPom file: '';
    echo "${readpom.groupId}"
    echo "${readpom.version}"
    }
    stage ('Code Analysis')
    {
        def sonarscannerhome = tool 'SonarQube Scanner'
        withSonarQubeEnv ('SonarQube Server') {
          sh """${sonarscannerhome}/bin/sonar-scanner """
        }
    }
}
