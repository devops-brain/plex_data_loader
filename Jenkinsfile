pipeline {
  agent none

  stages {
    stage('Generate or update symlink catalog of video masters') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_Movies/ -c ./convertMovies.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh '''for collection in Koi-Pond Rose-Garden Dragons-Den Donna-Collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in Koi-Pond Dragons-Den
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_TV/ -c ./convertTV.yml
        done'''
     }
    }
    stage('Generate or update symlink catalog of video masters on legacy infra') {
      agent {
        label "plex-shares"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py -i /srv/nfs/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/nfs/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_Movies/ -c ./convertMovies.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/nfs/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh '''for collection in Koi-Pond Rose-Garden Dragons-Den Donna-Collection Roger-Roger
        do
        python3 ./loadplexdata.py -i /srv/nfs/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in Koi-Pond Dragons-Den
        do
        python3 ./loadplexdata.py -i /srv/nfs/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_TV/ -c ./convertTV.yml
        done'''
      }
    }
    stage('unmanaged masters report') {
      agent {
        label "plex-shares"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py --report -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
      }
    }
  }
}
