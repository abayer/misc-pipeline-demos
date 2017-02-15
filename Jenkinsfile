// A Declarative Pipeline is defined within a 'pipeline' block.
pipeline {

  // agent defines where the pipeline will run.
  agent {
    // This also could have been 'agent any' - that has the same meaning.
    label ""
    // Other possible built-in agent types are 'agent none', for not running the
    // top-level on any agent (which results in you needing to specify agents on
    // each stage and do explicit checkouts of scm in those stages), 'docker',
    // and 'dockerfile'.
  }
  
  // The tools directive allows you to automatically install tools configured in
  // Jenkins - note that it doesn't work inside Docker containers currently.
  tools {
    // Here we have pairs of tool symbols (not all tools have symbols, so if you
    // try to use one from a plugin you've got installed and get an error and the 
    // tool isn't listed in the possible values, open a JIRA against that tool!)
    // and installations configured in your Jenkins master's tools configuration.
    jdk "jdk8"
    // Uh-oh, this is going to cause a validation issue! There's no configured
    // maven tool named "mvn3.3.8"!
    maven "mvn3.3.8"
  }
  
  environment {
    // Environment variable identifiers need to be both valid bash variable
    // identifiers and valid Groovy variable identifiers. If you use an invalid
    // identifier, you'll get an error at validation time.
    // Right now, you can't do more complicated Groovy expressions or nesting of
    // other env vars in environment variable values, but that will be possible
    // when https://issues.jenkins-ci.org/browse/JENKINS-41748 is merged and
    // released.
    FOO = "BAR"
  }
  
  stages {
    // At least one stage is required.
    stage("first stage") {
      // Every stage must have a steps block containing at least one step.
      steps {
        // You can use steps that take another block of steps as an argument,
        // like this.
        //
        // But wait! Another validation issue! Two, actually! I didn't use the
        // right type for "time" and had a typo in "unit".
        timeout(time: true, uint: 'MINUTES') {
          echo "We're not doing anything particularly special here."
          echo "Just making sure that we don't take longer than five minutes"
          echo "Which, I guess, is kind of silly."
          
          // This'll output 3.3.3, since that's the Maven version we
          // configured above. Well, once we fix the validation error!
          sh "mvn -version" 
        }
      }
      
      // Post can be used both on individual stages and for the entire build.
      post {
        success {
          echo "Only when we haven't failed running the first stage"
        }
        
        failure {
          echo "Only when we fail running the first stage."
        }
      }
    }
    
    stage('second stage') {
      // You can override tools, environment and agent on each stage if you want.
      tools {
        // Here, we're overriding the original maven tool with a different
        // version.
        maven "mvn3.3.9"
      }
      
      steps {
        echo "This time, the Maven version should be 3.3.9"
        sh "mvn -version"
      }
    }
    
    stage('third stage') {
      steps {
        // Note that parallel can only be used as the only step for a stage.
        // Also, if you want to have your parallel branches run on different
        // nodes, you'll need control that manually with "node('some-label') {"
        // blocks inside the parallel branches, and per-stage post won't be able
        // to see anything from the parallel workspaces.
        // This'll be improved by https://issues.jenkins-ci.org/browse/JENKINS-41334, 
        // which adds Declarative-specific syntax for parallel stage execution.
        parallel(one: {
                  echo "I'm on the first branch!"
                 },
                 two: {
                   echo "I'm on the second branch!"
                 },
                 three: {
                   echo "I'm on the third branch!"
                   echo "But you probably guessed that already."
                 })
      }
    }
  }
  
  post {
    // Always runs. And it runs before any of the other post conditions.
    always {
      // Let's wipe out the workspace before we finish!
      deleteDir()
    }
    
    success {
      mail(from: "bob@example.com", 
           to: "steve@example.com", 
           subject: "That build passed.",
           body: "Nothing to see here")
    }

    failure {
      mail(from: "bob@example.com", 
           to: "steve@example.com", 
           subject: "That build failed!", 
           body: "Nothing to see here")
    }
  }
  
  // The options directive is for configuration that applies to the whole job.
  options {
    // For example, we'd like to make sure we only keep 10 builds at a time, so
    // we don't fill up our storage!
    buildDiscarder(logRotator(numToKeepStr:'10'))
    
    // And we'd really like to be sure that this build doesn't hang forever, so
    // let's time it out after an hour.
    timeout(time: 60, unit: 'MINUTES')
  }

}
