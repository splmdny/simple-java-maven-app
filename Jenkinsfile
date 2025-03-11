// node {
//     // Declare agent and turn arg into inside
//     docker.image('maven:3.9.3').inside('-v /root/.m2:/root/.m2 --user=root') {
//         // Build
//         stage('Build') {
//             checkout scm
//             sh 'mvn -B -DskipTests clean package'
//         }
//         // Test
//         stage('Test') {
//             checkout scm
//             sh 'mvn test'
//             junit 'target/surefire-reports/*.xml'
//         }
//         //Deliver
//         stage('Deliver') {
//             checkout scm
//             sh './jenkins/scripts/deliver.sh'
//         }
//     }
// }

pipeline {
    agent {
        docker {
            image 'maven:3.9.3'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
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
                stage('Manual Approval') {
            steps {
                script {
                    def userInput = input(
                        message: 'Lanjutkan ke tahap Deploy?',
                        parameters: [choice(name: 'Confirm', choices: ['Proceed', 'Abort'], description: 'pilih opsi')]
                    )
                    if (userInput == 'Abort') {
                        error('Pipeline stopped')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                checkout scm
                sh './jenkins/scripts/deliver.sh'
                script {
                    echo 'Loading.. will ready in 1 minutes'
                    sleep(time: 60, unit: 'SECONDS')
                }
            }
        }
    }
}