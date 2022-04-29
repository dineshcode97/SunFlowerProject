pipeline {
  stages {
    stage('Compile') {
      steps {
        // Compile the app and its dependencies
        git branch: 'main', url: 'https://github.com/dineshcode97/sunflower.git'
      }
    }

    stage('Build APK') {
      steps {
        // Finish building and packaging the APK
        sh './gradlew assembleDebug'

        // Archive the APKs so that they can be downloaded from Jenkins
        archiveArtifacts '**/*.apk'
      }
    }
    stage('Static analysis') {
      steps {
        // Run Lint and analyse the results
        sh './gradlew lintDebug'
        //androidLint pattern: '**/lint-results-*.xml'
      }
    }
    stage('Deploy') {
      steps {
        // Build the app in release mode, and sign the APK using the environment variables
        sh './gradlew assembleRelease'

        // Archive the APKs so that they can be downloaded from Jenkins
        archiveArtifacts '**/*.apk'
      }
    }
  } 
}
