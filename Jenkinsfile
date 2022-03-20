pipeline {
    agent { label 'jdk11-mvn3.8.5' }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'this is maven goals')
        choice(name: 'BRANCH_TO_BUILD', choices: ['master', 'dev', 'prod'], description: 'These are all branches')
    }
        triggers {
        cron('*/55 * * * *')
        pollSCM('*/2 * * * *')
    }
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/Shri-1991/java11-examples.git', branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage('build') {
            steps {
                sh "/usr/local/apache-maven-3.8.5/bin/mvn ${params.MAVEN_GOAL}"
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