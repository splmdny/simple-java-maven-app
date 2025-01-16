node {
    // Declare agent and turn arg into inside
    docker.image('maven:3.9.0').inside('-v /root/.m2:/root/.m2') {
        // Build
        stage('Build') {
            checkout scm
            sh 'mvn -B -DskipTests clean package'
        }
        // Test
        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        //Deliver
        stage('Deliver') {
            checkout scm
            sh './jenkins/scripts/deliver.sh'
        }
    }
}