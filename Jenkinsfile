pipeline{
	agent any
	parameters{
		string(name: 'tomcat_dev', defaultValue: '54.234.247.3', description: 'Staging Server')
		string(name: 'tomcat_prod', defaultValue: '52.90.95.31', description: 'Production server')
	}
	triggers{
	pollSCM('* * * * *')
	}
	stages{
	   stage ("initialize") {
        steps {
            
            sh 'mvn checkstyle:checkstyle'
            }
          }
          stage ('Build project') {
            steps {
                sh "mvn clean install"
                 }
			}
		
	
	}
	}