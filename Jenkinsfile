pipeline {
    agent { label 'jdk11-mvn3.8.5' }
    parameters { string(name: 'BRANCH_BUILD', defaultValue: 'master', description: 'This Para') }
    triggers {
        cron('*/45 * * * *')
        pollSCM('*/2 * * * *')
    }
    stages {
        stage('scm') {
            steps {
                git url 'https://github.com/GitPracticeRepo/java11-examples.git', BRANCH_BUILD {$para.BRANCH_BUILD}
            }
        }
        stage('build') {
            steps {
                sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
            }
        }
        stage('archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
        stage('testreport11') {
            steps {
                junit '**/*.xml'
            }
        }
    }
}