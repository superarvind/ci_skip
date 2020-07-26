pipeline{
    agent any
    stages{
        stage('validate change log'){
            when {
                changelog '^(istio|release)+: [A-Z]{0,4}-[0-9]{0,5}\s+.*'
            }
            steps{
                script{
                    echo "CHANGE_ID : ${env.CHANGE_ID}"
                }
            }
        }
    }
}