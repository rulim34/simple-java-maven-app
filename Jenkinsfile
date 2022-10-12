node {
    checkout scm
    withDockerContainer(args: '-v /root/.m2:/root/.m2', image: 'maven:3.8.1-adoptopenjdk-11') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            withCredentials([gitUsernamePassword(credentialsId: 'heroku', gitToolName: 'Default')]) {
                sh 'git push https://git.heroku.com/simple-java-maven-app-falkia34.git HEAD:refs/heads/master -f'
            }
            sleep time: 1, unit: 'MINUTES'
        }
    }
}
