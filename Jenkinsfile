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
                                  sh "mvn sonar:sonar -Dsonar.projectKey=sonarqube -Dsonar.host.url=http://192.168.43.173:9000/ -Dsonar.login=f08317df87dd32274a4d5d9b210655c31f55d8ad"
                              }
                          }




         stage('nexus') {
            steps {

              script {

sh 'mvn -DskipTests deploy  -e'                      }
                   }
         }/*
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
                            } */
     }

     }
