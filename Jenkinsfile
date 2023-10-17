pipeline {
  agent none

  stages {
    stage('Generate or update symlink catalog of video masters in terminal') {
      agent {
        label "plex-shares"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh 'ls -hal /srv/masters*'
        sh '#python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_Movies/ -c ./convertMovies.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/temp -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '''for collection in koi-pond rose-garden dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in koi-pond dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_TV/ -c ./convertTV.yml
        done'''
     }
    }
    stage('Generate or update symlink catalog of video masters in k8s') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '''for collection in koi-pond rose-garden dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in koi-pond dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_TV/ -c ./convertTV.yml
        done'''
        sh 'python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_Movies/ -c ./convertMovies.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/temp -o /media/DVR_TV/ -c ./convertTV.yml'
     }
    }
    stage('unmanaged masters report') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py --report -i /srv/masters_DVR/PlayOn -o /media/DVR_TV/ -c ./convertTV.yml'
      }
    }
  }
}
