pipeline{
  agent{
    checkout scm
    docker.withRegistry("http://10.60.1.94:5000/"){
      docker.image("gcc-analyse").withRun("-v /var/lib/jenkins/workspace/gcc-analyse:/home/gcc-analyse"){
        echo "hello registry"
      }
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
}
