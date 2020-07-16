pipeline {
    agent any
    
     environment {
        sonar = "http://35.232.144.40:9000"
    }
	
    stages {
        stage('Code Checkout') {
            steps {
                echo 'Checkout'
            }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               	//def scannerHome = tool 'SonarQube Scanner 3.0'
			    withSonarQubeEnv('nambasonar') {  
				
				sh ''' curl -u admin:admin -X POST ""${sonar}/api/projects/create?"project=myproject&branch=${GIT_BRANCH#*/}&name=myproject-${GIT_BRANCH#*/}""" '''
				sh ''' curl -u admin:admin -d "projectKey=myproject:${GIT_BRANCH#*/}&gateId=3" -X POST ""${sonar}/api/qualitygates/select"" '''
				sh ''' curl -u admin:admin -d "projectKey=myproject:${GIT_BRANCH#*/}&profileName=test&language=java" -X POST ""${sonar}/api/qualityprofiles/add_project"" ''' 
				sh 'sleep 10'
				sh 'mvn clean install sonar:sonar -Dsonar.projectKey=myproject:${GIT_BRANCH#*/}'
			    }
		//     timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
           //         waitForQualityGate abortPipeline: true
          //  }
        }
	// stage('Quality Gate') {
        //     steps {
        //        timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
        //            waitForQualityGate abortPipeline: true
        //        }
        //    }
        }    
    }
}
