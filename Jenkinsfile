node {
    // Declare agent and turn arg into inside
    docker.image('maven:3.9.3').inside('-v $HOME/.m2:/var/maven/.m2:z -e MAVEN_CONFIG=/var/maven/.m2 -e MAVEN_OPTS="-Duser.home=/var/maven"') {
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