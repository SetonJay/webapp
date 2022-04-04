pipeline {
        agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                        echo "PATH = ${PATH}"
                        echo "M2_HOME = ${M2_HOME}"
                    '''
            }

        }

        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
            stage('Scan') {
                steps {
                        sh 'grype dir:. --scope AllLayers'
            }
        }
        
         stage ('Deploy-to-Tomcat') {
            steps {
                    sh '''
                                curl -v -u admin:admin -T /var/jenkins_home/workspace/WebApp-CICD-Pipeline/target/WebApp.war 'http://172.18.0.6:8080/manager/text/deploy?path=/webapps&update=true'
                        '''
                }
            }
        }

    }
