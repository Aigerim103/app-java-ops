pipeline {
    agent any
    parameters {
        booleanParam(name: 'DEPLOY', defaultValue: true, description: 'Czy uruchomić etap wdrożenia?')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building applications...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Applications...'
            }
        }
                stage(' Checkout ') {
                      steps {
                echo 'Checkout...'
            }
        }
                stage(' Compile  ') {
                      steps {
                echo 'Compile ...'
            }
        }
              stage(' Prepare Manifest   ') {
                      steps {
                echo 'Prepare Manifest  ...'
            }
        }
                     stage(' PPackage    ') {
                      steps {
                echo 'PPackage   ...'
            }
        }
                stage('Run') {
            when {
                expression { params.Run }
            }
            steps {
                echo 'Implementing applications...'
            }
        }
    }
}
