def registry = 'https://gayathrik.jfrog.io'
def imageName = 'gayathrik.jfrog.io/npm-docker-local/demo-nodejs'
def version   = '1.0.2'
pipeline{
    agent {
        node {
            label "Nodejs"
        }
    }
    tools {nodejs 'Nodejs'}

    stages {
        stage('build') {
            steps{
                echo "------------ build started ---------"
               	sh "npm install"
                echo "------------ build completed ---------"
        }
      }

        stage('Unit Test') {
            steps {
                echo '<--------------- Unit Testing started  --------------->'
                sh 'npm test'
                echo '<------------- Unit Testing stopped  --------------->'
            }
        }    
stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

    stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'Jfrog-npm')
                {
                    app.push()
             
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
           
    }
}    
