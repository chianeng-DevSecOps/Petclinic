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
                withSonarQubeEnv('sonar-server') {
                    sh ''' 
                    $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=petclinic \
                    -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=petclinic 
                   '''
                }
            }
        }

    post {  
        always {  
            echo 'This will always run'  
        }  
        success {  
            mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "SUCCESS CI: Project name -> ${env.JOB_NAME}", to: "nengchia01@gmail.com";  
        }  
        failure {  
            mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "nengchia01@gmail.com";  
        }  
        unstable {  
            echo 'This will run only if the run was marked as unstable'  
        }  
        changed {  
            echo 'This will run only if the state of the Pipeline has changed'  
            echo 'For example, if the Pipeline was previously failing but is now successful'  
        }  

    }
}

