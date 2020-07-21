node {
    stage('Checkout') {
        logger.stage()
        timeout(10) {
            checkout scm
        }
    }

    docker.image("murbanob9508/android_fastlane").inside {
        stage('Clean builds'){
            logger.stage()
            timeout(5){
                sh "gradle clean"
            }
        }
    }
}