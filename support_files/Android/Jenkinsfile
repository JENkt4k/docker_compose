pipeline {
  agent { 
    docker {
       image 'circleci/android:api-29-node' 
    }
  }
  stages {
    stage('clean') {
      steps {
          sh './gradlew clean'  
      }
    }
    stage('build') {
      steps {
          sh './gradlew build'
      }
    }
    stage('Sonarqube') {
      environment {
        scannerHome = tool 'SonarQubeScanner'
      }
      steps {
        withSonarQubeEnv('sonarqube') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 30, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
    stage('Lint and Unit Test'){
      parallel {
        stage('lint'){
          steps{
            script {
              try {
                sh './gradlew lint'
              } catch (Exception e) {
                echo e.getMessage()
                echo "Lint failed"
              }
            }       
          }
        }
        stage('test'){
          steps{
            script {
              try {
                sh './gradlew test'
              } catch (Exception e) {
                echo e.getMessage()
                echo "test failed"
              }
            }       
          }   
        }
      }
    }
    stage('createAPK'){
      steps{
        sh './gradlew assembleRelease'  
      }
    }
  }
  post {
    always {            
      junit 'app/build/test-results/**/*.xml'
      androidLint canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'app/build/reports/**/*', unHealthy: ''
      archiveArtifacts 'app/build/outputs/apk/**/*.apk'
      dir('app/build/test-results'){ 
        deleteDir()
      }
      
    }
  }
} 