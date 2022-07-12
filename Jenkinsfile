node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sh "cat /fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "sed -i 's+nexus-registry.eastus.cloudapp.azure.com:8085/fleetman-webapp.*+nexus-registry.eastus.cloudapp.azure.com:8085/fleetman-webapp.:${DOCKERTAG}+g' /fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "cat /fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "git add ."
                sh "git commit -m 'Jenkins Job change manifest: ${commit_id}'"
                sh "git push -u origin main"
            }
        }
    }
}