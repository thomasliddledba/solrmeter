node('buildciserver'){
    stage('Clean Workspace'){
        deleteDir()
    }
    stage('Checkout SCM'){
        checkout scm
    }
    stage('Build Development'){
        when{
            branch 'develop'
        }
        steps{
            sh('mvn package')
        }
    }
    stage('Build Production'){
        echo "Skipping for now"
    }
}// End of Node