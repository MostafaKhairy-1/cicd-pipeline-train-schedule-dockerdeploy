pipeline{
    agent any
    stages{
        stage ("build") {
            steps{
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage ("docker build"){
            when{
                branch "master"
            }
            steps {
            sh "docker build . -t mostafakhairy/my-repo  "
            withCredentials([usernamePassword(credentialsId: 'docker_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]){
            sh "echo "$USERPASS" | docker login --username USERNAME --password-stdin "
            sh "docker push mostafakhairy/my-repo:latest "
            }
            }
        }
       
    }
}
