node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build and Push Docker Image') {
        if(env.BRANCH_NAME == 'dev'){
            app = docker.build("saveska/kiii-jenkins")
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
    stage('Deploy to Production') {
        if(env.BRANCH_NAME == 'main'){
           
            // Deploy the application to production
            // ...
        }
    }
}
