#!/usr/bin/env groovy

pipeline {
    agent {
        node {
            label 'linuxvm'
        }
    }
    stages {
        stage('Setup up environment') {
            steps {
                sh 'npm install'
            }
        }
        stage('Cypress execution') {
            when {
                expression { params.SKIP_EXECUTION == false }
            }
            step{
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh "npx cypress run"  
                }
            }
        }
        // stage('Post Building Action') {
        //     when {
        //         expression { params.SKIP_EXECUTION == false }
        //     }
        //     steps {
        //             archiveArtifacts artifacts: '**/*.png', allowEmptyArchive: true, fingerprint: true
        //             archiveArtifacts artifacts: '**/*.mp4', allowEmptyArchive: true, fingerprint: true
        //     }
        // }
    }
}