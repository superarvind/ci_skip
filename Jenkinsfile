pipeline{
    agent any
    stages{
        stage('validate change log'){
            steps{
                script{
                    check('(istio|release)+: [A-Z]{2,4}-[0-9]{0,5}\\s+.*')
                }
            }
        }
        stage('next_stage'){
        when {
            anyOf {
                environment name: 'CI_SKIP', value: 'false'
                environment name: 'CI_SKIP', value: null
            }
        }
            steps{
                echo "In next_stage after CI commit check, and is working."
            }
        }
    }
}

def check(String regex) {
    try{
    env.CI_SKIP = "false"
    //result = sh (script: "git log --oneline -1 | grep -oE '(istio|release)+: [A-Z]{2,4}-[0-9]{0,5}\\s+.*'", returnStatus: true)
    result = sh (script: "git log --oneline -1 | grep -oE '${regex}' 2>/dev/null", returnStatus: true)
    echo "in check"
    if (result != 0) {
        env.CI_SKIP = "true"
        error "No matching pattern found in git commit message. Expected regex : '${regex}'"
    }
    }catch(e){
        //currentBuild.result = 'NOT_BUILT'
        //throw e
        env.CI_SKIP = "true"
    }
}
