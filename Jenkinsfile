node('buildciserver'){
    stage('Clean Workspace'){
        deletedir
    }
    stage('Checkout SCM'){
        checkout SCM
    }
    stage('Build'){
        sh('mvn package')
    }
}// End of Node