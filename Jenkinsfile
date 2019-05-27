pipeline {
  agent none

  stages {
    stage('Upload content'){
      parallel {
        stage('PlayOn Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('PlayOn Reformatted TV') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
          }
        }
        stage('PlayOn Format-Filtered TV') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
          }
        }
        stage('Roger-Roger MakeMKV Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Roger-Roger; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Rose-Garden MakeMKV Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Rose-Garden; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Donna-Collection MakeMKV Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Donna-Collection; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Dragons-Den MakeMKV Movies') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Dragons-Den; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Dragons-Den MakeMKV TV') {
          agent {
            label "plex-shares"
          }
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Dragons-Den; python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_TV/ -c ./convertTV.yml'
          }
        }
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
  }
}
