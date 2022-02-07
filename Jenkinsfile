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
    stage('Email Notification'){
      steps{
        mail bcc: '123456', body: '''Build successful!!!!
          Thanks,
          Mahesh''', cc: '', from: '', replyTo: '', subject: 'Build successfull', to: 'talha.tasci@pavotek.com.tr'
      }
    }
    stage("Notify Jira"){
      steps{
        echo "bbbbbb"
        jiraSendBuildInfo branch: 'JD-1', site: 'jenkins-demo.atlassian.net'
        def transitionInput = [
          transition:[
            id: '1'
          ]
        ]
        jiraTransitionIssue idOrKey: "JD-1", input: transitionInput        
      }
    }
  }

}
