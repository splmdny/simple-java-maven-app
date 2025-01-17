node {
    // Declare agent and turn arg into inside
    docker.image('maven:3.9.3').inside('-v /root/.m2:/root/.m2 --user=root') {
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

// Check Poll SCM 1
// Check Poll SCM 2