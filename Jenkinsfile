pipeline {
    agent any


    stages {


        stage('MVN CLEAN') {
            steps {

              script {

                  sh 'mvn  clean'


                      }
                   }
         }
          stage('MVN compile') {
            steps {

              script {

                  sh 'mvn compile'


                      }
                   }
         }
          stage('MVN test') {
            steps {

              script {

                  sh 'mvn  test'


                      }
                   }
         }

          stage('Artifact Construction') {
                      steps{
                          sh "mvn -B -DskipTests  package "
                      }
                  }
                  stage('sonar') {
                              steps{
                                  sh "mvn sonar:sonar -Dsonar.projectKey=sonarqube -Dsonar.host.url=http://192.168.43.39:9000/ -Dsonar.login=ecb992930386104c558ea90932766d50418571f7"
                              }
                          }




         stage('nexus') {
            steps {

              script {

sh 'mvn -DskipTests deploy  -e'                      }
                   }
         }
        stage('Build Docker Image'){
                      steps {
                          script{
          				    sh 'docker image build  -t yass1ne/backcicd .  '
                          }
                      }
          		}
          		stage('Docker login') {
                                steps {
                                    script {

                                        sh 'docker login -u yass1ne -p Y@$$1ne@1997 '}
                                }
                                }

                          stage('Pushing Docker Image') {
                                steps {
                                    script {

                                     sh 'docker push yass1ne/backcicd'
                                    }
                          }
                          }

                          stage('Run Spring && MySQL Containers') {
                                steps {
                                    script {
                                      sh 'docker-compose up -d'
                                    }
                                }
                            }
     }

     }
