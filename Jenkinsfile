pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        sh 'aws s3 cp build/libs/application.war s3://joohyun-cicd-jenkins-deploy/application.war --region ap-northeast-2'
      }
    }

    stage('deploy') {
      steps {
        sh 'aws elasticbeanstalk create-application-version --region ap-northeast-2 --application-name joohyun-cicd-test-1 --version-label ${BUILD_TAG} --source-bundle S3Bucket="joohyun-cicd-jenkins-deploy",S3Key="application.war"'
        sh 'aws elasticbeanstalk update-environment --region ap-northeast-2 --environment-name joohyun-cicd-test-1-sample --version-label ${BUILD_TAG}'
      }
    }

  }
}
