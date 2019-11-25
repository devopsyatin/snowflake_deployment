pipeline {
    options {
      timeout(time: 1, unit: 'HOURS') 
			}
  agent {
    docker {
      image 'yatu10/snowflake-sqitch_21nov'
      args "-u root -v /var/run/docker.sock:/var/run/docker.sock --entrypoint=''"
		   }
		}
  stages {
    stage('Verifying Prerequisite Versions') {
        steps {
            sh '''
	   	snowsql -v
		sqitch --version
		whoami
		hostname
            ''' 
        }
	  }
	  
    stage('Verifying Sqitch Configs') {
    	steps{
    		sh '''
	      sqitch config --user engine.snowflake.client /bin/snowsql
	      sqitch config --user user.name 'amrutdengre'
              sqitch config --user user.email 'amrutdengre@gmail.com'
	      cat ~/.sqitch/sqitch.conf
	      cat sqitch.conf
	      cat sqitch.plan
	      hostname
	      #sqitch add appschema -n 'Add schema for all snowjenkinstest objects.'
	      cat deploy/appschema.sql
	          '''
               
    		}
	}
    stage('Deploy changes to SampleDB') {
      steps {
           sh '''
	      hostname
	      cat deploy/appschema.sql
	      sqitch deploy 'db:snowflake://amrutdengre:NewStart123@vxa95806.us-east-1.snowflakecomputing.com/DEMO_DB?Driver=Snowflake'
              '''           
        }
      }
   
    stage('Verify changes to SampleDB') {
      steps {
           sh '''
              sqitch verify 'db:snowflake://amrutdengre@vxa95806.us-east-1.snowflakecomputing.com/DEMO_DB?Driver=Snowflake'
              ''' 
        }
      }
    }   
post {
    always {
      sh 'chmod -R 777 .'
    }
  }
  }
