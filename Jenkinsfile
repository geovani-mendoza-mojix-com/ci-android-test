#!groovy

node() {
    environment {
     username = 'Geovani'
   }
    checkout scm
    stage('Greeting'){
        echo 'Hello Mr. ${username}'
    }
}