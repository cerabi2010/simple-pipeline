node('maven') {
  stage('Build') {
    sh " oc whoami"
    sh " pwd ; id;"
    git url: "https://github.com/Heesun-Yang/simple-pipeline.git"
    sh "mvn package"
    sh "ls  *"
  }
  
  stage('Test') {
    parallel(
      "Cart Tests": {
        sh "curl -s -X POST http://simple:8080/index.jsp"
      },
      "Discount Tests": {
        sh "curl -s -X POST http://simple:8080/failover.jsp"
      }
    )
  }
  
  stage('Build Image') {
    sh "oc start-build simple --from-file=target/ROOT.war --follow"
  }
  
  stage('System Test') {
    sh " sleep 30"
    sh "curl -s http://simple:8080/index.jsp"
  }
}
