pipeline {
  agent none

  stages {
    stage('Upload content'){
      parallel {
        stage('Roger_Roger MakeMKV Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Roger_Roger; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Rose_Garden MakeMKV Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Rose_Garden; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Donna_Collection MakeMKV Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Donna_Collection; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Dragons_Den MakeMKV Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Dragons_Den; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Koi_Pond MakeMKV Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Koi_Pond; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('Dragons_Den MakeMKV TV') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Dragons_Den; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/TV/ -c ./convertTV.yml'
          }
        }
        stage('Koi_Pond MakeMKV TV') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'collection=Koi_Pond; python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/TV/ -c ./convertTV.yml'
          }
        }
        stage('PlayOn Movies') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/Movies/ -c ./convertMovies.yml'
          }
        }
        stage('PlayOn Reformatted TV') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/TV/ -c ./convertTV.yml'
          }
        }
        stage('PlayOn Format-Filtered TV') {
          agent any
          steps {
            echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            sh 'python3 ./loadplexdata.py --dvr -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/TV/ -c ./convertTV.yml'
          }
        }
      }
    }
  }
}
