pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'stg', 'prod'],
            description: 'Select the environment'
        )
    }

    stages {
        stage('Hello World') {
            steps {
                echo "Hello World from trigger ${params.ENVIRONMENT}"
            }
        }

        stage('Hello Jenkins') {
            steps {
                echo "Hello Jenkins from ${params.ENVIRONMENT}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
    emailext(
        subject: "[FAILED] ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        mimeType: 'text/html',
        body: """
        <h2>Jenkins Build Failed</h2>

        <table border="1" cellpadding="5">
            <tr><td><b>Job</b></td><td>${env.JOB_NAME}</td></tr>
            <tr><td><b>Build</b></td><td>#${env.BUILD_NUMBER}</td></tr>
            <tr><td><b>Environment</b></td><td>${params.ENVIRONMENT}</td></tr>
            <tr><td><b>Triggered By</b></td><td>${currentBuild.getBuildCauses()[0].shortDescription}</td></tr>
        </table>

        <br>
        <a href="${env.BUILD_URL}">Open Build</a>
        """,
        attachLog: true,
        compressLog: true,
        to: "waleeddarwesh2002@gmail.com"
    )
}
    }
}
