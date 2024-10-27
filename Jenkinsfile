node {
    def application = "akil-springbootapp"
    def dockerhubaccountid = "akil1991"
    def image

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        image = docker.build("${dockerhubaccountid}/${application}:${BUILD_NUMBER}")
    }

    stage('Push image') {
        withDockerRegistry([credentialsId: "dockerHub", url: ""]) {
            image.push()
            image.push("latest")
        }
    }

    stage('Deploy to Kubernetes') {
        kubernetesDeploy (configs: 'deployment.yaml' ,kubeconfigId: 'kubeconfig-credentials-id')
    }
}
