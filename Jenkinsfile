pipeline {
    agent {
        node {
            label "linux && java17"
        }
    }
    stages {
        stage("hello") {
            steps {
                echo("hello pipeline")
            }
        }
    }
}