node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build and Push Docker Image') {
        when {
            branch 'dev'
        }
        steps {
            app = docker.build("saveska/kiii-jenkins")
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
    stage('Deploy to Production') {
        when {
            branch 'main'
        }
        steps {
            // Deploy the application to production
            // ...
        }
    }
}
