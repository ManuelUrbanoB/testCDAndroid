node {
    stage('Checkout') {
        timeout(10) {
            checkout scm
        }
    }

    docker.image("murbanob9508/android_fastlane").inside {
        stage('Clean builds'){
            timeout(10){
                sh "gradle clean"
            }
        }

        stage('setup credentials'){
            timeout(5){
                 withCredentials([string(credentialsId: 'android_keystore_cd_ci_test', variable: 'android_keystore')]) {
                     sh """cat > $WORKSPACE/keystore.jks_64 <<  EOL\n$android_keystore\nEOL"""
                     sh "base64 -d keystore.jks_64 > app/keystore.jks"
                }
            }
        }

        stage('Create APK') {
            timeout(10){
                sh 'gradle bundleRelease'
            } 
        }

        stage('Archive AAB'){
            timeout(10){
                dir("app/build/outputs/bundle") {
                    sh "mv release/app-release.aab release/app-release-${BUILD_NUMBER}.aab"
                    archiveArtifacts "release/app-release-${BUILD_NUMBER}.aab"
                }
            }
        }
        
        stage('Clean credentials'){
            timeout(10){
                sh "rm app/keystore.jks"
            } 
        }
    }
}