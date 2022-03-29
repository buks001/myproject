pipeline {
    agent any
    
     environment {
        GIT_URL = 'main', url: 'https://github.com/buks001/myproject.git'
        TOMCAT_URL   = 'http://34.236.149.216:8080/
    }
    
    stages {
        stage('git checkout') {
            steps {
              git branch: $"{GIT_URL}"
            }
        }
         stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
          stage('Deploy to tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: $"{TOMCAT_URL}")], contextPath: 'myapp', war: '**/*.war'
            }
        }
    }
}
