node {
    stage('Clone repository') {
        checkout scm
    }    
    stage('Update GIT') {
        script {
            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                sh "cat fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "sed -i 's+nexus-registry.eastus.cloudapp.azure.com:8085/fleetman-webapp.*+nexus-registry.eastus.cloudapp.azure.com:8085/fleetman-webapp.:${DOCKERTAG}+g' fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "cat fleetman/develop/fleetman-webapp-deploy.yaml"
                sh "git add ."
                sh "git commit -m 'Jenkins Job change manifest: ${DOCKERTAG}'"
                sh "git push https://github.com/MKH-Beldi/fleetman-k8s-manifests.git HEAD:main"
            }    
        }
    }
    
}