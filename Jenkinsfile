node {
    stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
        git url: 'ssh://git@ssh.github.com:443/osrerf/lab01.git', credentialsId: 'e9ad14ae-9831-4db9-8d1f-198d95117aa4'
    }
    stage('Build') {
        // Run the maven build
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
