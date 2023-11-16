pipeline {
  agent any
  stages {
    stage('Cloner le dépôt') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/nickjj/docker-node-example.git']]])
      }
    }

    stage('Construire l\'image Docker') {
      steps {
        script {
          docker.build('test-image-jenkins')
        }

      }
    }
post {
    always {
      script {
        discordSend(
          description: "Le build a ${currentBuild.result}",
          result: currentBuild.result,
          title: env.JOB_NAME,
          webhookURL: "https://discord.com/api/webhooks/1174662484783812672/TSOs8sAUV14BBsJlQ1oOJyLRzdHKfdMr9mrbqBJr1PZQ1o3X8lpDbjtR8mvOQnHxVkMc"
        )
      }
    }

  }
  }
}
