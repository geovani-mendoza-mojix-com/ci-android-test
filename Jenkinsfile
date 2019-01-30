#!groovy

node() {
    checkout scm
    try {
        stage('Compile') {
            sh './gradlew compileDebugSources'
            printStatus()
        }

        stage('Static analysis') {
            sh './gradlew lintDebug'
            printStatus()
        }

        stage('Static analysis') {
            sh './gradlew lintDebug'
            androidLint pattern: '**/lint-results-*.xml'
        }
    } finally {
        stage('Build APK') {
            sh './gradlew assembleDebug'
            archiveArtifacts '**/*.apk'
            printStatus()
        }
    }
}

def printStatus() {
    if (currentBuild.result == 'FAILURE') {
        echo "BUILD STATUS: FAILURE"
    } else {
        echo "BUILD STATUS: SUCCESS"
    }
}