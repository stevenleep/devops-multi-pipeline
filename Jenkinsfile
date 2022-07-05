pipeline {
    agent any
    triggers {
        githubPush()
    }
    parameters {
        string(
            name: "name",
            description: "Name of the pipeline",
            defaultValue: "pipeline",
            // required: true
        )
        string(
            name: "description",
            description: "Description of the pipeline",
            defaultValue: "Pipeline description",
            // required: true
        )
    }

    stages {
        stage('Pull resources from github') {
            steps {
                echo "start pulling resources from github"
                sh "whoami"
            }
        }
    }
}
