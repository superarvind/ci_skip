pipeline{
    agent any
    stages{
        stage('validate change log'){
            steps{
                script{
                    this.check()
                }
            }
        }
        stage('next_stage'){
            steps{
                echo "In next_stage after CI commit check, and is working"
            }
        }
    }
}

def check() {
    try{
    env.CI_SKIP = "false"
    result = sh (script: "git log --oneline -1 | grep -oE '(istio|release)+: [A-Z]{2,4}-[0-9]{0,5}\\s+.*'", returnStatus: true)
    if (result != 0) {
        env.CI_SKIP = "true"
        echo "No matching pattern found in git commit message. Expected regex (istio|release)+: [A-Z]{2,4}-[0-9]{0,5}\\s+.*'"
        error "NOT_BUILT"
    }
    }catch(e){
        throw e
        currentBuild.result = 'SUCCESS'
        
    }
}