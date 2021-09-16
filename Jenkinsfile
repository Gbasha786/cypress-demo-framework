pipeline {
    agent any
    parameters {
        string(name: 'SPEC', defaultValue: 'cypress/integration/**/**', description: 'Ej: cypress/integration/pom/*.spec.js')
        choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'], description: 'Pick the web browser you want to use to run your scripts')
    }
    
    options {
        ansiColor('xterm')
    }

    stages {
        stage('Regression Execution') {
            steps {
                echo "SPEC ${params.SPEC}"

                echo "BROWSER: ${params.BROWSER}"
                bat "npm i"
                bat "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
                slackSend channel: 'jenkins-example', message: 'Automation Build From Jenkins Started'
            }
        }
        stage('Publish HTML Report'){
            steps {
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'cypress/report', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
                slackSend channel: 'jenkins-example', message: 'Automation Build Finished'
            }
        }
    }
}
