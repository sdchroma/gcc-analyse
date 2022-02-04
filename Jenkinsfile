pipeline{
  agent{    
    docker{
      image "10.60.1.94:5000/gcc-analyse"
      args "-v /var/lib/jenkins/workspace/gcc-analyse:/home/gcc-analyse"
    }
  }
  stages{
    stage("Lint test"){
      steps{
        sh "clang-format --dry-run --Werror /home/gcc-analyse/demo.c"
      }
    }
    stage("Static Analyse"){
      steps{
        sh "cppcheck /home/gcc-analyse/demo.c --enable=all --addon=/home/Misra/misra.json --xml > report.xml"
      }
    }
    stage("Build"){
      steps{
        sh "make"
      }
    }
  }
  post{
    success{
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
    }
    failure{
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'

    }
  }
}
