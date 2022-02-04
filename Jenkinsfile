pipeline{
  agent{
    docker {
      image "gcc-analyse"
    }
  }
  stages{
    stage("Lint test"){
      steps{
        sh "clang-format --dry-run --Werror./demo.c"
      }
    }
    stage("Static Analyse"){
      steps{
        sh "cppcheck" ./demo.c --enable=all --addon=/home/Misra/misra.json --xml > report.xml"
      }
    }
    stage("Build"){
      steps{
        sh "make"
      }
    }
  }
}
