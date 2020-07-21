node {
    stage('Checkout') {
        timeout(10) {
            checkout scm
        }
    }

    docker.image("murbanob9508/android_fastlane").inside {
        stage('Clean builds'){
            timeout(5){
                sh "gradle clean"
            }
        }
    }
}