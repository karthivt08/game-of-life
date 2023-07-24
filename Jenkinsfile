pipeline{

    agent {
        label 'Jenkins-node1'
    }
    options {
        timeout(time: 1, unit: 'HOURS')
    }

    triggers {
        pollSCM('* * * * *')
    }

    parameters {
        choice(name: 'Maven_Goal', choices: ['clean', 'clean package', 'install', 'deploy'], description: 'Maven Goal')
    }
    tools {
        jdk 'JDK8'
    }
stages {
    stage ('Source Code Checkout') {
        steps {
            git branch: 'master',
            url: 'https://github.com/karthivt08/game-of-life.git'
        }
    }

    stage ('Build')
    {
        steps {
            sh "mvn ${Maven_Goal}"
        }
    }

    stage ('report stage') {
        steps {
            archiveArtifacts artifacts: '**/target/gameoflife*.war'
                junit testResults: '**/target/surefire-reports/TEST-*.xml'

        }
    }
}

}
