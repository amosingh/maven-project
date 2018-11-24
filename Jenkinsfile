pipeline{
	agent any
	stages{
		stage(test){
			steps{
				sh '''
						echo "PATH = ${PATH}"
						echo "M2_HOME = ${M2_HOME}"
				   '''


	}
	}
	stage ('Build') {
	    steps {
	    		sh 'mvn clean package'
	    }
	    post {
	    success {
	    echo 'now Archiving'
	    archiveArtifacts artifacts: '**/target/*.war'
	    }
	    }
	}
	}
}