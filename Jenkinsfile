pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'ubuntu@localhost:/home/ubuntu/AUTOMATE_WITH_JENKINS/dev_tomcat', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'ubuntu@localhost:/home/ubuntu/AUTOMATE_WITH_JENKINS/prod_tomcat', description: 'Production Server')
    }

    triggers {
         pollSCM('*/1 * * * *')
     }

         tools {
             maven 'Maven-3.6.0'
         }

stages{
            stage('Checkout') {
            steps {
                checkout(
					[$class: 'GitSCM',
					 branches: [[ name: "$GIT_COMMIT" ]],
					 extensions: [],
					 userRemoteConfigs: [[credentialsId: 'Github-App-Pwd', url: 'https://github.com/prasadrahul/automate_with_jenkins.git']]
					]
                )
            }
        }
            stage('Build'){
                steps {
                    sh 'mvn clean package -Pci'
                }
                post {
                    success {
                        echo 'Tick Tick Now Archiving...'
                        archiveArtifacts artifacts: '**/target/*.war'
                    }
                }
            }

//            stage ('Deployments'){
//                parallel{
//                    stage ('Deploy to Staging'){
//                        steps {
//                            sh "scp **/target/*.war ${params.tomcat_dev}/webapps"
//                        }
//                    }
//
//                    stage ("Deploy to Production"){
//                        steps {
 //                           sh "scp **/target/*.war ${params.tomcat_prod}/webapps"
 //                       }
 //                   }
 //              }
 //           }    
        }
    
        post {
        always {
    //        junit testResults: '**/target/surefire-reports/TEST-*.xml'

     //       recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
     //       recordIssues enabledForFailure: true, tool: spotBugs()
     //       recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
     //       recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
    //        recordIssues aggregatingResults: true, minimumSeverity: 'NORMAL', qualityGates: [[threshold: 0, type: 'TOTAL_ERROR', unstable: false]], unhealthy: 0
        }
    }
}
