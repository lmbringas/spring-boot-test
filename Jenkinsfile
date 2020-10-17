pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        git(url: 'https://github.com/lmbringas/spring-boot-test.git', branch: 'main', poll: true)
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
        junit 'target/*.jar'
      }
    }

  }
}

pipeline {
    agent any
    tools {
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                git(url: 'https://github.com/lmbringas/spring-boot-test.git', branch: 'main', poll: true)
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
