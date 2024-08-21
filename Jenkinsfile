pipeline {
  agent any

  stages {
    stage('Clone Repository') {
      steps {
        deleteDir()  // Clean workspace before cloning (optional)
        git branch: 'main', url: 'https://github.com/JPYADAV96/python-mysql-db-proj-1.git'
      }
    }

    stage('Build') { 
      steps { 
        withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
          script {
            app = docker.build("my-ecr-repo")
          }
        }
      }
    }

    stage('Push') {
      steps {
        script {
          docker.withRegistry('https://129390742221.dkr.ecr.eu-central-1.amazonaws.com','ecr:eu-central-1:aws-credentials') {
            app.push("latest")
          }
        }
      }
    }
  }
}
