node{

		// defining variable for maven home directory
		def mavenHome = tool name: "maven 3.8.4"
		echo "The node name is ${env.NODE_NAME}
		echo "The Job name is ${env.JOB_NAME}
		echo "The Build number is ${env.BUILD_NUMBER}
	
		// Getting code from Git
		stage('CheckoutCode'){
		git branch: 'development', credentialsId: '8e2e3f97-73b4-49e2-b3f9-43929e5f3699', url: 'https://github.com/Konda-Motorcycles/maven-web-application-1.git'
		}
	
	
		// Generating build
		stage('Build'){
		sh "$mavenHome/bin/mvn clean package"
		// bat command for wondows
		}
		
		//SonarQube report
		stage('Sonarqube report'){
		sh "$mavenHome/bin/mvn sonar:sonar"
		}
		
		//Upload Artifact into Artifactory repo
		stage('Nexus'){
		sh "$mavenHome/bin/mvn deploy"
		}
		
		//Deploying to Tomcat Server
		stage('Tomcat Deployment'){
		sshagent(['189fdc90-1915-49fb-bb3b-19a43f11f3e4']) {
		// some block
		sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.111.147.9:/opt/apache-tomcat-9.0.76/webapps"
		}
		}
	

	} //Node closing
