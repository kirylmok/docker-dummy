pipeline {
    agent any

    stages {
        stage ('Clone') {
            steps {
                checkout scm
            }
        }

        stage ('Build docker image') {
            steps {
                script {
                    docker.build
                }
            }
        }

        stage ('Push image to Artifactory') {
            steps {
                rtDockerPush(
                    serverId: "Artifactory",
                    image: 'kirylm.jfrog.io/default-docker-local/alpine-curl:latest',
                    targetRepo: 'default-docker-local',
                    properties: 'project-name=docker-dummy-m;status=running'
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Artifactory"
                )
            }
        }
    }
}
