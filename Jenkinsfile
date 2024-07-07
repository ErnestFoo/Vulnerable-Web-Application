pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
    stage ('Checkout') {
            steps {
            git branch:'master', url: 'https://github.com/ErnestFoo/Vulnerable-Web-Application.git'
            }
        }
    stage('Code Quality Check via SonarQube') {
        steps {
            script {
                def scannerHome = tool 'SonarQube';
                withSonarQubeEnv('SonarQube') {
                    sh "/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner \
                        -Dsonar.projectKey=OWASP \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://192.168.50.157:9000 \
                        -Dsonar.token=ssqp_8da9339aaecb0f9fe921ad6378cf6a0466d979a9"
                }
            }   
        }
    }
    }
    post {
        always {
        recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
