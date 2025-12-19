pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/LohadeDarshan/Deploying-a-Python-Web-Application.git'
            }
        }
        stage('code validate') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'   // validate the code
                }
            }
        }
        stage('code compile') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'   // compile
                }
            }
        }
        stage('code test') {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn test'   // test
                }
            }
        }
        stage('build the code') {
      steps {
        withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
          sh 'mvn clean package'
        }
      }
    }
        stage('deploy to tomcat server'){
            steps {
                sshagent(['DevCICD']){
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war root@10.162.98.210:/var/lib/tomcat10/webapps'
                }
            }
        }
    }
}
