#!groovy
// @Library('utils@master') _

def APPENVC
def MAJOR_VERSION = "1";
def ARTIFACT_VERSION = "${MAJOR_VERSION}.${BUILD_NUMBER}";


node {

      stage('Git Checkout'){
            checkout scm develop
      }
      
    //   //garantizar que librerias y paquetes, existan
      stage('Preparation') {
          // for display purposes
          //1. necesito instalacion de npm
        //   sh 'npm --version'
        //   //2. garantizar que la version de aws corresponde
        //   sh 'aws --version'
        //   //3. clonar todo el proyecto (al principio se clona unicamente el jenkinsfile
        //   //3.  instalar dependencias del proyecto
        //   //sh 'npm install & npm install yarn'
        //   //sh 'yarn install'
        sh 'npm install'
        //   sh 'mkdir -p layer/nodejs'
        //   sh 'cp package.json layer/nodejs/'
        //   sh 'cd layer/nodejs/ && npm install'

          //4. validar version de serverless
        sh 'sls --version'
        //5. escribir en el log la ubicacion actual de la ejecucion
        sh 'pwd'
        sh 'ls'
        sh 'dir'
      }
      stage('Build') {
      /*
      *aca se hace la construccion del proyecto
      *deployToDev es un metodo generado por el equipo de kyle Labbe para el despliegue hacia entorno
      *de desarrollo
      */
            echo JOB_NAME
            withAWS(credentials:'test', region:'us-east-1') {
                //   sh 'export SLS_DEBUG=true'
                  //testing dir
                //   sh 'dir'
                  //testing file structure
                //   sh 'ls'
                  
                  //deploy lambda, dynamodb
                  sh "sls deploy -v --stage ${APPENVC}"

                  
            }
      }
    //   if( APPENVC == 'nonprod' && PROMPROD == 'Y'){
    //         stage('zipping Files'){
    //         sh "zip -r br_earnix_api.zip . -x '*layer*/*' -x '*git*/*' -x '*serverless*/*' -x '*nodeModulesDependencies*'"
    //         }

    //         stage('Upload to Artifactory'){
    //               def artifacts = [
    //               'br_earnix_api.zip']
    //               artifactoryUploadFiles files:artifacts,version:ARTIFACT_VERSION
    //               promoteToProd(email:'Marcelo.Baes@libertyseguros.com.br, SilviaCR@libertyseguros.com.br, AntonioG@libertyseguros.com.br', version:ARTIFACT_VERSION) {
                  
    //               }
            
    //         }
    //   }
}
