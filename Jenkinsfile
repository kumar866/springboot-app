pipeline {
    agent any
    tools{
        maven "Maven"
    }

    stages {
        stage('git check out') {
            steps {
             git branch: 'main', url: 'https://github.com/kumar866/springboot-app.git'
            }
        }
        stage("build"){
            steps{
                sh "mvn clean install"
            }
        }
        stage ('JaCoCo') {
      steps {
      jacoco()
          }
        }
        stage("build image"){
            steps{
              sh "docker build -t kumarramya/springboot-app:1 ."  
            }
        }
        stage("docker loginand push"){
            steps{
                script{
                   withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) {
                     sh "docker login -u kumarramya -p ${Docker_Hub_Pwd}"
                     } 
                    sh "docker push kumarramya/springboot-app:1 " 
                }
            }
        }
    }
}
