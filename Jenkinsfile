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
    } catch (e) {
        // If there was an exception thrown, the build failed
        currentBuild.result = "FAILED"
        throw e
    } finally {
        // Success or failure, always send notifications
        stage('Build APK') {
            sh './gradlew assembleDebug'
            archiveArtifacts '**/*.apk'
            printStatus()
        }
        notifyBuild(currentBuild.result)
    }
}