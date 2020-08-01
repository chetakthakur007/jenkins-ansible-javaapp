pipeline {
    agent {
        label "master"
    }

    tools {
        maven "M2"
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/chetakthakur007/jenkins-ansible-javaapp.git'

                sh "mvn -f app/pom.xml -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    archiveArtifacts 'app/target/*.war'
                }
            }
        }
        stage('deploy'){
            steps{
                ansiblePlaybook credentialsId: 'webhostid', installation: 'ansible', inventory: 'deployment/environment.ini', playbook: 'deployment/tomcat.yml'
            }
        }
    }
}
