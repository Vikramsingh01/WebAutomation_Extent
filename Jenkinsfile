pipeline {
    agent any
    tools {
        maven 'Maven 3.6.3'
        jdk 'jdk8'
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
                withMaven(maven : 'maven_3_6_3') {
                sh 'mvn clean compile'
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