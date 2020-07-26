pipeline{
    agent any
    stages{
        stage('validate change log'){
            steps{
                check
            }
        }
        stage('next_stage'){
            steps{
                echo "In next_stage"
            }
        }
    }
}

def check() {
    env.CI_SKIP = "false"
    result = sh (script: "git log --oneline -1 | grep -oE '^(istio|release)+: [A-Z]{0,4}-[0-9]{0,5}\\s+.*'", returnStatus: true)
    if (result != 0) {
        env.CI_SKIP = "true"
        error "'[ci skip]' found in git commit message. Aborting."
        currentBuild.result = 'NOT_BUILT'
    }
}