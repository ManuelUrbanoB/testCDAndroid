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
                 withCredentials([file(credentialsId: 'android_keystore', variable: 'android_keystore')]) {
                     sh "mv $android_keystore > app/keystore.jks"
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