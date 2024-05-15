pipeline {
  agent any

  tools {
    maven 'M2_HOME'
    }
  
  stages {
    stage('Checkout') {
      steps {
        echo 'Checkout the source code from GitHub'
        git branch: 'main', url: 'https://github.com/Boogey123sahu/star-agile-banking-finance.git'
            }
    }
    stage('Package') {
      steps {
        echo 'Create a Package'
        sh 'mvn clean package'
             }
          }
    stage('Publish Test Reports') {
       steps {
         publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/BankingProject/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
             }
          }

    stage('Create Image using the package') {
       steps {
         echo 'creating a docker image from the package'
         sh 'docker build -t kailashsahu/banking:1.0 .'
              }
           }
    stage('Docker Login') {
       steps {
          echo 'Login to Docker hub to push the images'
          withCredentials([usernamePassword(credentialsId: 'Dockerlogin-user', passwordVariable: 'Dockerpassword', usernameVariable: 'Dockerlogin')]) {
          sh 'docker login -u ${Dockerlogin} -p ${Dockerpassword}'
                                                 }
                           }
              }
    stage('Push the Image') {
       steps {
          sh 'docker push kailashsahu/banking:1.0'
                            }
             }
  
     }
    
}
