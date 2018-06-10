node('buildciserver'){
    stage('Clean Workspace'){
        deleteDir()
    }
    stage('Checkout SCM'){
        checkout scm
    }
    stage('Build'){
        sh('mvn package')
    }
}// End of Node