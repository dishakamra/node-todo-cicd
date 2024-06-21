node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/dishakamra/node-todo-cicd.git', branch: 'master' 
    }

     stage("Build") {

       sh 'docker build . -t dishavk/node-todo-test:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u dishavk -p Feb26####'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push dishavk/node-todo-test:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml'
    }
}
