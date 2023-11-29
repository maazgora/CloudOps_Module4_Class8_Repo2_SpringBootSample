pipeline {
    agent { 
        node {
            label 'Java-Node'
        }
    }
    parameters {
        choice(
            choices: ['true' , 'false'],
            description: 'Do you wish to save the jar after the build?',
            name: 'SAVE_JAR')
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('check workspace details') {
            steps {
                sh 'pwd && ls -lrt'
            }
        }  
        stage('copy latest jar'){
            when {
                expression { params.SAVE_JAR == 'true' }
            }          
            steps {
                sh 'mkdir -p ~/jars && cp ./target/*.jar ~/jars'
            }
        }
    }
    post {
        success {
            echo 'Job completed successfully'
        }
        failure {
            echo 'Job failed'
        }
    }
}
