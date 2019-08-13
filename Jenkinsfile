#!groovy

pipeline ()
{
	//GitHub 
	
	stage('checkout')
	{
		git credentialsId: 'Github', url: 'https://github.com/DevOps-Training-Tools/Maven-multi-project.git'
	}
	
	//Maven Lifecycle
	
	stage('Maven Build')
	if(isUnix())
		{
			sh 'mvn clean validate'
		}
	else
		{
			bat 'mvn clean validate'
		}
	stage('Maven compile')
	if(isUnix())
		{
			sh 'mvn compile'
		}
	else
		{
			bat 'mvn compile'
		}
	stage('Maven test')
		if(isUnix())
		{
			sh 'mvn test'
		}
		else
		{
			bat 'mvn test'
		}
	stage('Maven Package')
	if(isUnix())
	{
		sh 'mvn package'
	}
	else
	{
		bat 'mvn package'
	}
	
	//SonarQube Testing
	stage('SonarQube')
		if(isUnix())
		{
			sh 'mvn sonar:sonar'
		}
		else
		{
			bat 'mvn sonar:sonar'
		}
	//To store maven local Repository
	stage('Maven install')
		is(isUnix())
		{
			sh 'mvn install'
		}
		else
		{
			bat 'mvn install'
		}
	
	//To store Maven Remote Repository
		stage('Maven deploy')
		if(isUnix())
		{
			sh 'mvn deploy'
		}
		else
		{
			bat 'mvn deploy'
		}
	
	// To Deploy the code into tomcat
		
/*
	stage('build Image')
	{
		sh 'docker build -t imagename .'
	}
	stage('Image Push')	
	{
		sh 'docker login -u username -p password'
		sh 'docker push URL:imagename'
	}
	stage('Deploy Cont')
	{
		sh 'docker service create -d -p 8080:8080 --name container1 -v valumename:/data/db --mode=global imagename
	}
	
	*/
	stage('To Deploy Tomcat')
		if(isUnix())
		{
			sh 'cp $WORKSPACE/target/*.war /opt/apache-tomcat-9.0.22/webapps'
		}
		else
		{
			bat 'copy %WORKSPACE%/target/* C:/programfiles/Apache-tomcat/webapps/'
		}	
		//Email configuration
		
		stage('Email')
		{
		emailext attachLog: true, body: '''$Project nameand $Project Build number


			Thanks& Regards
			Charan
			9177932721''', compressLog: true, recipientProviders: [developers()], replyTo: 'charan2721@gmail.com', subject: 'Projectname_Build number', to: 'Charan2721@gmail.com'
		}
}
