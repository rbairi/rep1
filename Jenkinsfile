pipeline {
    // agent { docker { image 'python:3.5.1' } }
    agent any
    stages {
        stage('build') {
            steps {
                // sh 'python --version; echo hello world;'
                sh """
                echo HELLO WORLD
                echo TESTING MULTILINE HELLO WORLD
                pwd
                ls -l
                
                """
            }
        }
    }
}
