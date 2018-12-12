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
		 maven "M2_HOME"
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
                sh "/usr/local/bin/docker build -t tomcatwebapp:1.0 ."
                 }
			}
		
	
	}
	}