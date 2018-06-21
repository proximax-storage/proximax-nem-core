pipeline {
    agent {
        docker {
            image 'maven:3.5.3-jdk-8'
            args '-v /home/ubuntu/.m2:/root/.m2'
        }
    }

    // using the Timestamper plugin we can add timestamps to the console log
    options {
        timestamps()
    }

    stages {
        stage('Build') {
            steps {
                // check the version
                sh 'mvn --version'
                // build and package
                sh 'mvn -B -DskipTests clean package'
            }
        }
//        stage('Test') {
//            steps {
//                // Run the tests
//                sh 'mvn test'
//            }
//            post {
//                always {
//                    junit 'target/surefire-reports/*.xml'
//                }
//            }
//        }

        stage('Deploy Snapshot') {
            steps {
                sh 'mvn deploy -DskipTests -DaltDeploymentRepository="nexus::default::https://nexus.internal.proximax.io/repository/maven-snapshots"'
            }
        }
    }
}