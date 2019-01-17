pipeline {
	  
	  tools {
	    maven 'Maven-3'
	    jdk 'Java-8'
	  }
	  agent any 
	  
	  stages {
	    stage ('Compile') {
	      steps {
	        echo 'In Compile'
	        sh 'mvn clean install'
		      script {
			     result = sh (script: "git log -1 | grep '.*\\[NM-\\].*'", returnStatus: true)
			      echo 'Result of Grep'
			      echo result
		      }
	      }
	      post {
	        always {
			//emailext body: 'Build phase completed !!!', subject: 'Build Completed', to: 'santosh.narate@gmail.com, kunalpise@gmail.com'
	          
			//junit "**/TEST-*.xml"
	        }
	       }
	     }
	     
	    stage('Static Analysis & Code Review') {
	       steps {
		       echo 'in Static Analysis Phase'
	            //sh 'mvn sonar:sonar'
	         
	       }
	     }
	     stage ('Deploy on QA Env') {
	              steps {
	                     echo 'Smoke Test'
	                     //sh 'mvn test -PSmoke'
	              }
	       }
	    stage ('QA Phase') {
	              steps {
	                     echo 'Testing on QA environment'
	                     echo 'Regression Test'
	                     //sh 'mvn test -PRegression'
	             
	              }
	    }
		    
		    stage ('QA Email') {
	              steps {
	                    // emailext body: 'This email to test Pipeline.', subject: 'Email to test Pipeline', to: 'kpise@searshc.com'
	             
	              }
          
	       }
	  }
	}
