pipeline {
    agent any
    tools {
        maven 'a maven'
        jdk 'JDK 8'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

     stage ('Compile Stage') {
            steps {
                withMaven(maven : 'a maven') {
                sh 'mvn clean compile'
                }
            }
       }
	   
	    stage ('maven test') {
            steps {
                withMaven(maven : 'a maven') {
                sh 'mvn test'
                }
            }
       }


        stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}