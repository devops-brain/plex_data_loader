pipeline {
  agent none

  stages {
    stage('Upload content'){
      parallel {
        stage('Koi-Pond MakeMKV Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Koi-Pond; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Koi-Pond MakeMKV TV') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Koi-Pond; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_TV/ -c ./convertTV.yml'
          }
        }
      }
    }
    stage('unmanaged masters report') {
      agent {
        label "plex-shares"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'python3 ./loadplexdata.py --report -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
      }
    }
  }
}
