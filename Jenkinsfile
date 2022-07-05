pipeline {
    agent any
    // This trigger will be fired when the pipeline is first created.
    triggers {
        // github webhook trigger
        githubPush()
    }
    parameters {
        string(
            name: "MONITOR_SERVICE_URL",
            description: "Please enter the DSN provided for the monitoring service.",
            defaultValue: "",
            // required: true
        )
        string(
            name: "APP_SERVER_URL",
            description: "app service address",
            defaultValue: "https://dev.simi.com",
            required: true
        )
        string(
            name: "NGINX_CONF_PATH",
            description: "nginx conf path",
            defaultValue: "nginx.conf",
            required: true
        )
    }
    // this environment apply to all steps within the Pipeline
    environment {
        BUILD_USER = "jenkins-branlice",
    }

    stages {
        stage('Start') {
            steps {
                echo "---- start build step -----"
                githubStatusNotify buildState: "DOWNLOADING"
                git branch: "${params.BRANCH}", url:"https://github.com/appcenter/app"
                // global: custom git subcommand
                sh 'git inspect resources:"$params.BRANCH"'
                console state:"DOWNLOADED" // echo "resources downloaded successfully"
            }
        }
        stage('Build') {
            steps {
                githubStatusNotify buildState:"BUILDING"
                npmChecker version:"<= 16.15.1", automaticInstaller: "default"
                sh "npm config set registry $TAO_BAO_REGISTRY"

                // console state:"START_INSTALL_DEPS"
                sh "npm install"

                // sh "npm run build"
                /**
                * TODO: sed 替换配置文件中的环境变量
                */

                sh '[-d $BUILD_DIR] && { echo "$BUILD_DIR found"; }'

                githubStatusNotify buildState:"COMPILE_BUILD"
                sh '[ -f /deployment/nginx.conf ] && { echo "nginx.conf found"; cp "$FILE" /tmp/$APP_NAME_$params.BRANCH }'
            }
        }

        stage("Test") {
            steps {
                echo "start testing"
                sh "whoami"
            }
        }
        stage("Deploy") {
            steps {
                echo "start deploying"
                sh "whoami"
            }
        }
        stage("Report") {
            steps {
                echo "start ending"
                sh "whoami"
            }
        }
    }
}
