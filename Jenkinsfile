pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/alekhya167/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t alekhya1607/phpimgv2 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push alekhya1607/phpimgv2'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                script{
                    sh 'sudo docker run -itd --name My-project-con -p 8089:80 alekhya1607/phpimgv2'
                       }
                    }
                }
    }
}
