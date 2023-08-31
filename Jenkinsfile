pipeline {
    agent any
    tools{
        maven 'maven3'
        jdk 'jdk17'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git-Checkout') {
            steps {
               git branch: 'develop', url: 'https://github.com/chianeng-DevSecOps/Petclinic.git'
            }
        }
        stage('Code-Compile') {
            steps {
               sh "mvn compile" 
            }
        }
        stage('Test-Cases') {
            steps {
               sh "mvn test"
            }
        }
        stage('Build-Artifact') {
            steps {
               sh "mvn clean package"
            }
        }
        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' 
                    $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=demo2 \
                    -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=demo2 
                   '''
                }
            }
        }
    }
}
