pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/RAVITEJA12344/Amazon-Prime-Video.git',credentialsId: 'github-creds'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('SonarQube') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=amazon-prime-video \
                    -Dsonar.projectKey=amazon-prime-video '''
                }
            }
        }
        stage("quality gate"){
           steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token' 
                }
            } 
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }        
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build -t amazon-prime-video ."
                       sh "docker tag amazon-prime-video:latest ravi1224/amazon-prime-video:latest "
                       sh "docker push ravi1224/amazon-prime-video:latest "
                    }
                }
            }
        }
		/*
		stage('Docker Scout Image') {
            steps {
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                       sh 'docker-scout quickview ravi1224/amazon-prime-vide:latest'
                       sh 'docker-scout cves ravi1224/amazon-prime-video:latest'
                       sh 'docker-scout recommendations ravi1224/amazon-prime-video:latest'
                   }
                }
            }
        }
		*/

        stage("TRIVY-docker-images"){
            steps{
                sh "trivy image ravi1224/amazon-prime-video:latest > trivyimage.txt" 
            }
        }
        stage('App Deploy to Docker container'){
            steps{
                sh '''
          		   docker stop amazon-prime-video || true
         		   docker rm amazon-prime-video || true
         		   docker run -d --name amazon-prime-video -p 3000:3000 ravi1224/amazon-prime-video:latest
      		    '''
            }
        }

    }
	/*
    post {
    always {
        script {
            def buildStatus = currentBuild.currentResult
            def causes = currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')
            def buildUser = causes ? causes[0].userId : 'GitHub Trigger'

            emailext(
                subject: "Pipeline ${buildStatus}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <p><b>Amazon Prime Video CI/CD Pipeline Status</b></p>
                    <p><b>Project:</b> ${env.JOB_NAME}</p>
                    <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> ${buildStatus}</p>
                    <p><b>Triggered By:</b> ${buildUser}</p>
                    <p><b>Build URL:</b>
                      <a href="${env.BUILD_URL}">${env.BUILD_URL}</a>
                    </p>
                """,
                to: 'ravitejaravirala2@gmail.com',
				from: 'ravitejaravirala2@gmail.com',
                replyTo: 'ravitejaravirala2@gmail.com',
                mimeType: 'text/html',
                attachmentsPattern: '**/trivy*.txt',
                attachLog: true
            )
        }
       }

    }
*/
post {
    always {
        emailext(
            to: 'ravitejaravirala2@gmail.com',
            subject: "Jenkins Job ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
            body: "Build URL: ${env.BUILD_URL}"
        )
    }
}


}
