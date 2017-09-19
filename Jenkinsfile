node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"
    imageName = "rakatti/mulesoftesb:latest"
    env.BUILDIMG=imageName

    stage "Build"
    
        sh "docker build -t ${imageName} mule381"
    
    stage "Push"

        sh "docker push ${imageName}"

    stage "Deploy"

        sh "kubectl apply -f deploy.yml"
        sh "kubectl rollout status deployment/mule-deployment"
        sh "kubectl apply -f service.yml"
        sh "kubectl get services"
}
