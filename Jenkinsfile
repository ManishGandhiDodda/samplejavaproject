pipeline{
	tools{
	maven = tool name: 'M3', type: 'maven'
	sonarhome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
	}
	agent any
	stages{
    	stage('checkout')
    	{
    	steps{
        	git 'git@github.com:ManishGandhiDodda/samplejavaproject.git'
        	workspace = pwd()
        	}
    	}
    	stage('Build')
    	{
    		steps{
        //	mvnHome = tool name: 'M3', type: 'maven'
        	withMaven(maven: 'M3', tempBinDir: '') {
        	sh 'mvn clean install'
        	}
        	}
    	}
    	stage('Code Analysis using Sonarqube')
    	{
    		steps{
        //	workspace = pwd()
        //	sonarHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
        	withSonarQubeEnv('SonarQube Server') {
            sh "${sonarHome}/bin/sonar-scanner"
			}
        	}
    	}
    	stage('Deploy onto Tomcat')
    	{
    	steps{
        echo "Deployement stage"
        sh 'cp ./multi-module/webapp/target/*.war /usr/local/apache-tomcat-9.0.19/webapps'
     //   sh "find . -iname "*.war" -exec cp {} /usr/local/apache-tomcat-9.0.19/webapps \;"
    	}
    	}
    }
}
