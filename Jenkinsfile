pipeline {
    agent any
    tools {
        jdk 'Java 21' // Match this to your Jenkins tool name
    }

    environment {
        JAVA_HOME = tool 'Java 21'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Aigerim103/app-java.git', branch: 'main',
            }
        }

        stage('Compile') {
            steps {
                bat 'if not exist build\\classes mkdir build\\classes'
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Main.java'
            }
        }

        stage('Prepare Manifest') {
            steps {
                bat 'echo Main-Class: Main > build\\classes\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
                bat 'if not exist build\\jar mkdir build\\jar'
                bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/jar/*.jar', fingerprint: true
        }
        cleanup {
            deleteDir()
        }
    }
}
