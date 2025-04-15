pipeline {
    agent any

    tools {
        jdk 'Java'
    }

    environment {
        JAVA_HOME = tool 'Java'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Aigerim103/app-java.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                bat '"%JAVA_HOME%\\bin\\javac" d built\classes Main.java'
            }
        }
    }
}
