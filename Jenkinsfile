pipeline {
    agent any

    environment {
        GITHUB_CREDS = credentials("GITHUB")
        IMAGE_NAME = "mariusmihai69/flask-app"
        GITHUB_REPO_NAME = "jenkins-k8s-manifests.git"
        GITHUB_USER_EMAIL = "mariusmihai.learning@gmail.com"
    }

    parameters {
        string(name: "IMAGE_TAG", description: "Docker Image Tag")
    }

    stages {
        stage("Update Manifest files") {
            steps {
                sh """
                git config user.email $GITHUB_USER_EMAIL
                git config user.name $GITHUB_CREDS_USR
                cat app.manifest.yml
                sed -i "s%$IMAGE_NAME:[0-9]*%$IMAGE_NAME:$IMAGE_TAG%g" app.manifest.yml
                cat app.manifest.yml
                git add .
                git commit -m 'Updated container image tag with value $IMAGE_TAG'
                git push https://$GITHUB_CREDS_USR:$GITHUB_CREDS_PSW@github.com/$GITHUB_CREDS_USR/$GITHUB_REPO_NAME HEAD:main
            """
            }
        }
    }
}

// git push https://$GITHUB_CREDS_USR:$GITHUB_CREDS_PWD@github.com/$GITHUB_CREDS_USR/$GITHUB_REPO_NAME HEAD:main