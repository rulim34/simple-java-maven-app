node {
    checkout scm
    withDockerContainer(args: '-v /root/.m2:/root/.m2', image: 'maven:3.8.1-adoptopenjdk-11') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
    }
}
