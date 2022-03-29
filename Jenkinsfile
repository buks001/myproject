pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/buks001/myproject.git'
            }
        }
		 stage("SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonar') {
                sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
              }
            }
          }
         stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
          stage('Deploy to tomcat') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://34.236.149.216:8080/')], contextPath: 'myapp', war: '**/*.war'
            }
        }
    }
}
