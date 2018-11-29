pipeline{
	agent any
	parameters{
		string(name: 'tomcat_dev', defaultValue: '54.234.247.3', description: 'Staging Server')
		string(name: 'tomcat_prod', defaultValue: '52.90.95.31', description: 'Production server')
	}
	triggers{
	pollSCM('* * * * *')
	}
	tools {
		 maven "MAVEN_HOME"
         jdk "JAVA_HOME"
	}
	stages{
	   stage ("initialize") {
        steps {
             sh '''
                 echo "PATH = ${PATH}"
                 echo "M2_HOME = ${M2_HOME}"
                
                '''
            }
          }
          stage ('Build project') {
            steps {
                 sh 'mvn clean package'
                 }
			}
		
	post{
	success{
	echo 'Now Archiving...'
	archiveArtifacts artifacts: '**/target/*.war'
	}
	}
	}
	stage ('Deployment'){
	parallel{
	stage ('Deploy to Staging'){
	steps {
	sh "scp -i /Users/amodkumar139153GMAILCOM/Downloads/KubernetesAWS.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
	}
	}
	stage ("Deploy to Production"){
	steps {
	sh "scp -i /Users/amodkumar139153GMAILCOM/Downloads/KubernetesAWS.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
	}
	}
	}
	}
	}