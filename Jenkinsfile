pipeline {
    agent any

    tools {
        jdk 'Java'  // Use the actual name defined in Jenkins
    }

    environment {
        JAVA_HOME = tool 'Java'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Aigerim103/app-java-ops.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                bat '''
                    if not exist built\\classes mkdir built\\classes
                    "%JAVA_HOME%\\bin\\javac" -d built\\classes Main.java
                '''
            }
        }

        stage('Prepare Manifest') {
            steps {
                bat '''
                    echo Main-Class: Main > built\\classes\\manifest.txt
                '''
            }
        }

        stage('Package') {
            steps {
                bat '''
                    if not exist built\\jar mkdir built\\jar
                    "%JAVA_HOME%\\bin\\jar" cfm built\\jar\\MyApplication.jar built\\classes\\manifest.txt -C built\\classes .
                '''
            }
        }

        stage('Run') {
            steps {
                bat '"%JAVA_HOME%\\bin\\java" -jar built\\jar\\MyApplication.jar'
            }
        }
    }
}
