pipeline {
    agent any

    tools {
        // Use the JDK version named "Java 21" configured in Jenkins
        jdk 'Java 21'
    }

    environment {
        JAVA_HOME = tool 'Java 21'
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Aigerim103/app-java.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                bat '''
                    if not exist build\\classes mkdir build\\classes
                    dir /s /b
                    "%JAVA_HOME%\\bin\\javac" -d build\\classes src\\Main.java
                '''
            }
        }

        stage('Prepare Manifest') {
            steps {
                bat 'echo Main-Class: Main > build\\classes\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                bat '''
                    if not exist build\\jar mkdir build\\jar
                    cd build\\classes
                    "%JAVA_HOME%\\bin\\jar" cvfm ..\\jar\\MyApplication.jar MANIFEST.MF *
                '''
            }
        }

        stage('Run') {
            steps {
                bat '''
                    echo Running the Java application...
                    "%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar
                '''
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed. Please check the console output for details.'
        }
        success {
            echo '✅ Build and run completed successfully.'
        }
    }
}

