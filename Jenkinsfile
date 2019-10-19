#!/usr/bin/groovy
//commenting 
import java.net.URL
import hudson.model.*
node {
   stage ('Checkout'){
      git 'https://github.com/edureka-git/DevOpsClassCodes.git'
   }
   stage('Compile'){
      withMaven(maven: 'TrainingMaven') {
    sh 'mvn compile'
}
   }
   stage ('Review'){
       withMaven(maven: 'TrainingMaven') {
    sh 'mvn pmd:pmd'
}
         }
         stage ('Test') {
       try 
       {
           withMaven(maven: 'TrainingMaven') {
    sh 'mvn test'
} }finally{
         junit 'target/surefire-reports/*.xml'

}
}
stage ('Metrics') {
       try 
       {
           withMaven(maven: 'TrainingMaven') {
    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
} }finally{
         cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false

}
}
  stage('package')  
{
    withMaven(maven: 'TrainingMaven') {
sh 'mvn package'
    }
    }  
}
