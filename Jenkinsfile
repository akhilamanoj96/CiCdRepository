pipeline {
    agent any

    environment {
        ANDROID_SDK_ROOT = "/Users/akhilamanoj/Library/Android/sdk"
        FLUTTER_HOME  = "/Users/akhilamanoj/development/flutter_3.24.3/flutter"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/akhilamanoj96/CiCdRepository.git',
                    credentialsId: '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'
            }
        }

        stages {
                stage('Flutter Doctor') {
                    steps {
                        sh '''
                          export PATH="$FLUTTER_HOME/bin:/usr/bin:/bin:/usr/sbin:/sbin"
                          flutter --version
                          flutter doctor
                        '''
                    }
                }
            }

        stage('Get Dependencies & Test') {
            steps {
                sh 'flutter pub get'
                sh 'flutter test'
            }
        }

        stage('Build Android APK') {
            steps {
                sh 'flutter build apk --release'
            }
        }

        // Optional: add iOS build if you use macOS + Xcode
        stage('Build iOS') {
            steps {
                sh 'flutter build ios --release --no-codesign'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build/app/outputs/**/*.apk', fingerprint: true
            cleanWs()
        }
    }
}
