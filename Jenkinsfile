pipeline {
    agent any


    stages {


        stage('MVN CLEAN') {
            steps {

              script {

                  sh 'mvn  clean'


                      }
                   }
         }/*
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
         }*/

          stage('Artifact Construction') {
                      steps{
                          sh "mvn -B -DskipTests  package "
                      }
                  }
        
                  stage('sonar') {
                              steps{
                                  sh "mvn sonar:sonar -Dsonar.projectKey=sonarqube -Dsonar.host.url=http://172.20.10.6:9000/ -Dsonar.login=d8ef234e92f92c5c88cfd3d2d2f1289e3e6e2ec1"
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
          				    sh 'docker image build  -t zwazwa/backcicd .  '
                          }
                      }
          		}
          		stage('Docker login') {
                                steps {
                                    script {

                                        sh 'docker login -u zwazwa -p zwazwa123'}
                                }
                                }

                          stage('Pushing Docker Image') {
                                steps {
                                    script {

                                     sh 'docker push zwazwa/backcicd'
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
