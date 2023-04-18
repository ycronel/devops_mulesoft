pipeline {
    agent any
    environment {
        ANYPOINT = credentials('ANYPOINT')
    }
    triggers {
        pollSCM('H/2 * * * *') 
    }
    stages {
        stage('Build') {
            steps {
                withMaven(maven:'maven') {
                    sh 'mvn -f mule-jenkins-pipeline/pom.xml clean install'
                }
            }
        }
        stage('Deploy') {
            steps {
                withMaven(maven:'maven') {
                    sh 'mvn -f mule-jenkins-pipeline/pom.xml package deploy -Dusername=$ANYPOINT_USR -Dpassword=$PASSWORD_PSW -Denvironment=Development -DmuleDeploy'
                }
            }
        }
    }
}