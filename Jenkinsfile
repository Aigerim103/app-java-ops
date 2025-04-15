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
                // Packaging compiled classes into a JAR file with a manifest file
                bat 'if not exist build\\jar mkdir build\\jar'
                // Uses a direct path to the manifest file located in buildclasses
                bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run') {
            steps {
                // Running an application from a JAR file
                bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
    }
}
