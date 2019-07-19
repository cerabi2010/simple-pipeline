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
        sh "curl -s -X POST http://simple:8080/simple/index.jsp"
      },
      "Discount Tests": {
        sh "curl -s -X POST http://simple:8080/simple/failover.jsp"
      }
    )
  }
  
  stage('Build Image') {
    sh "git clone https://github.com/Heesun-Yang/jeus8-simple"
    sh "echo 'Current:'; pwd "
    sh "cp -f target/simple.war jeus8-simple/"
    sh "oc start-build simple --from-dir=jeus8-simple --follow=true"
  }
  
  stage('System Test') {
    sh " sleep 30"
    sh "curl -s http://simple:8080/simple/index.jsp"
  }
}
