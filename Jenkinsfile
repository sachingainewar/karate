pipeline {
    agent any
        tools { 
                maven 'maven' 
                jdk 'jdk8' 
            }
    
    

    stages {
            stage('clean_workspace_and_checkout_source') {
              steps {
                deleteDir()
         
              }
            }
        stage('Build') {
            steps {
                git branch: 'develop', credentialsId: '1d106335-b1ef-4c93-964c-77fb9732dc9c', url: 'https://bitbucket.cashpoint.services/scm/qa/tabookieworld.git'
            }
        }
        stage ('Initialize') {
            steps {
                withMaven(maven : 'maven'){
                    sh'ls *'
                    sh "cd tabookieworld"
                    sh'ls *'
                    sh'pwd'
                }
                dir('tabookieworld/karateAPI'){
                    sh "pwd"
                    sh "mvn clean -Dtest=ParalleltestRunner install"
                }
            }

        }
		stage('Reporting System'){
		    steps{
		        cucumber buildStatus: "UNSTABLE",
		         jsonReportDirectory: 'tabookieworld/karateAPI/target/karate-reports/',
		        fileIncludePattern: "**/*.json"
		       
		    }
		}
		
	}
}
