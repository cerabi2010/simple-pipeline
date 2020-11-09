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
        sh "echo 'ok'"
      },
      "Discount Tests": {
        sh "echo 'ok'"
      }
    )
  }
  
  stage('Build Image') {
    sh "git clone https://github.com/Heesun-Yang/jeus8-simple"
    sh "echo 'Current:'; pwd "
    sh "cp -f target/simple.war jeus8-simple/"
    sh "oc start-build jws-app --from-dir=jeus8-simple --follow=true"
  }
  
  stage('System Test') {
    sh " sleep 30"
    sh "curl -s https://jenkins-cicd.apps.ocp3.example.com/"
  }
}
