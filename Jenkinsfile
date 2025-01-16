node {
    // Declare agent and turn arg into inside
    docker.image('maven:3.9.0').inside('-v /root/.m2:/root/.m2') {
        // Build
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // Test
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        //Deliver
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}