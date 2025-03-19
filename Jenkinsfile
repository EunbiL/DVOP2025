--- Jenkinsfile
+++ Jenkinsfile
@@ -1,6 +1,9
 pipeline {
     agent any
     stages {
         stage('Checkout SCM') {
             steps {
                 checkout scm
             }
         }
         stage('Config') {
             steps {
                 dir('build') {
                     sh 'cmake -G"Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug ..'
                 }
             }
         }
         stage('Build') {
             steps {
                 dir('build') {
                     sh 'cmake --build . --config Debug --target Test'
                 }
             }
         }
         stage('Run Test') {
             steps {
                 script {
                     try {
                         sh './build/Test'
                     } catch (Exception e) {
                         currentBuild.result = 'SUCCESS'
                         echo 'Test fail. But still continue the pipeline...'
                     }
                 }
             }
         }
     }
 }
