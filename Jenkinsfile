// Based on:
// https://raw.githubusercontent.com/redhat-cop/container-pipelines/master/basic-spring-boot/Jenkinsfile

library identifier: "pipeline-library@v1.5",
retriever: modernSCM(
  [
    $class: "GitSCMSource",
    remote: "https://github.com/redhat-cop/pipeline-library.git"
  ]
)

// The name you want to give your Application
// Each resource related to your app will be given this name
appName = "hello-java-spring-boot"

pipeline {
    // Use the 'maven' Jenkins agent image which is provided with OpenShift 
    // checkout and build Source code (SoringBoot in this example)
    agent { label "maven" }
    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }
        stage("Docker Build") {
            steps {
                // This uploads your application's source code and performs a binary build in OpenShift
                // This is a step defined in the shared library (see https://github.com/redhat-cop/pipeline-library.git)
                // (Or we could invoke this step using 'oc start-build <build config>' commands!)
                binaryBuild(buildConfigName: appName, buildFromPath: ".")
            }
        }

        // We could extend the pipeline by tagging the image,
        // or deploying it to a production environment, etc......
    }
}
