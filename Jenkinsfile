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
	      }
	      post {
	        always {
	          junit "**/TEST-*.xml"
	        }
	       }
	     }
	     
	    stage('Static Analysis & Code Review') {
	       steps {
	         parallel (
	           a : {
	            echo 'in Static Analysis Phase'
	            sh 'mvn sonar:sonar'
	           },
	           b : {
	             echo 'In Code Review Phase'
	             input('Does the code review successful?')
	           }
	              )
	       }
	     }
	     stage ('Deploy on QA Env') {
	              steps {
	                     echo 'Deploying on QA environment'
	              }
	       }
	    stage ('QA Phase') {
	              steps {
	                     echo 'Testing on QA environment'
	                     input ('Does the testing pass?')
	              }
	       }
	  }
	}
