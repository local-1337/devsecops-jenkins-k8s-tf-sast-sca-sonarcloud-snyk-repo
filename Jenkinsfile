pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2' 
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=host -Dsonar.organization=host -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=3fa6b2c6fb21c9d93f3e29da47606a882d095fe8'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
