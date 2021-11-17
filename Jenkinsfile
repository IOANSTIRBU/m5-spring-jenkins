pipeline {
    agent any
    tools {
        maven "Maven-3.8.3"
        jdk "jdk-17.0.1"
    }
    stages {

        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Site') {
            steps {
                bat 'mvn site'
            }
        }
        stage('Site'){
            steps {
                bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=m5-spring-jenkins-ioan -Dsonar.login=${env.SONAR_M5_SPRING_JENKINS} -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=ioanstirbu'
            }

        }

    }
}