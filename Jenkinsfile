echo "hello world"

// declarative pipeline
pipeline {
    agent any
    
    stages {
        stage("checkout") {
            steps {
                    git branch:'main', url: 'https://github.com/unmeshpawar/course3-jenkins-gs-spring-petclinic' 
            }
        }
        stage("build"){
            steps {
                bat "mvn package"    
            }
        }
        stage("capture"){
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }        
    }

    post {
        always {
            emailext body: '${env.BUILD_URL}\n${currentBuild.absoluteUrl}',
            to: 'always@foo.bar',
            recipientProviders: [previous()],
            subject: '${currentBuild.currentResult}: Job ${env.JOB_Name} [${env.BUILD_NUMBER}]'
        }
    }
}
