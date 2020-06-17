# Jenkins file 

## Jekinsfile example

```
pipeline {
    agent any 
    triggers {
        cron('H */4 * * 1-5')
    }
    tools {
        maven 'apache-maven-3.0.1' 
    }
       parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages {
        stage('Build') { 
            steps {
                // 
            }
        }
        stage('Test') { 
            steps {
                // 
            }
        }
        stage('Deploy') { 
            steps {
                // 
            }
        }
        stage('Example Deploy') {
            when { // execute if condition true
                branch 'production'
                environment name: 'DEPLOY_TO', value: 'production'
            }
            steps {
                echo 'Deploying'
            }
        }
        stage('Parallel In Sequential') {
                    parallel {
                        stage('In Parallel 1') {
                            steps {
                                echo "In Parallel 1"
                            }
                        }
                        stage('In Parallel 2') {
                            steps {
                                echo "In Parallel 2"
                            }
                        }
                    }
                }
        }
     post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}

```

## Jenkins on Kubernetes
```
#!/usr/bin/groovy

timestamps { 
  podTemplate(
    label: 'jenkins-pipeline', 
    inheritFrom: 'default',
    containers: [
      containerTemplate(name: 'docker', image: 'docker:18.06', command: 'cat', ttyEnabled: true),
      containerTemplate(name: 'chrome', image: 'garunski/alpine-chrome:latest', command: 'cat', ttyEnabled: true),
      containerTemplate(name: 'selenium', image: 'selenium/standalone-chrome:3.14', command: '', ttyEnabled: false, ports: [portMapping(containerPort: 4444)]),
    ]
  ) {
    node ('jenkins-pipeline') {
      stage('latest code') {
        checkout scm
      }

      container ('chrome') {
        stage('Install packages') {
          sh 'npm install --quiet'
        }

        stage('Linters') {
          sh 'npm run lint'
        }

        stage('Build') {
          sh 'npm run build'
        }

        stage('Run Unit Tests') {
          sh 'npm run test-ci'
          junit 'test-results/**/*.xml'
        }
      } //end container chrome

      stage('Run Code Coverage') {
      }

      stage('Deploy Local') {
        container('docker') { 
          sh "echo \$'FROM nginx:stable-alpine \nCOPY ./dist /usr/share/nginx/html \n' > Dockerfile"
          sh 'docker build -t jobrm:latest .' 
        }

        container('helm') {
          sh 'helm upgrade --install --force jobrm-static ./charts/jobrm-static --set image.repository=jobrm --set image.tag=latest --set service.type=NodePort --set service.nodePort=31001' 
        }
      } //end deploy local

      stage('Run e2e test') {
        container ('chrome') {
          sh 'npm test'
        }
        junit 'e2e/test-results/**/*.xml'
      }

      stage('Deploy Production') {
      }

      stage('Run Post Deployment Tests') {
      }
    } // end node
  } // end podTemplate
} // end timestamps

```
