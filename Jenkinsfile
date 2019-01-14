pipeline {
  agent any

  stages {
    stage('MakeMKV Movies') {
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'for collection in Roger_Roger Rose_Garden Donna_Collection Dragons_Den Koi_Pond; do python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml; done'
      }
    }
    stage('MakeMKV TV') {
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'for collection in Dragons_Den Koi_Pond; do python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/TV/ -c ./convertTV.yml; done'
      }
    }
    stage('PlayOn Movies') {
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'python3 ./loadplexdata.py -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/Movies/ -c ./convertMovies.yml'
      }
    }
    stage('PlayOn TV') {
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'python3 ./loadplexdata.py -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/TV/ -c ./convertTV.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters/DVR/PlayOn -o /srv/plexmedia/DVR/TV/ -c ./convertTV.yml'
      }
    }
  }
}
