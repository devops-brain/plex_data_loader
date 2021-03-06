pipeline {
  agent none

  stages {
    stage('Generate or update symlink catalog of video masters in k8s') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_Movies/ -c ./convertMovies.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/temp -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '''for collection in koi-pond rose-garden dragons-den donna-collection roger-roger
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in koi-pond dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_TV/ -c ./convertTV.yml
        done'''
     }
    }
    stage('sync masters from legacy') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '''rsync -Havu /srv/nfs/masters_Roger-Roger/* /srv/masters_roger-roger/
              rsync -Havu /srv/nfs/masters_Rose-Garden/* /srv/masters_rose-garden/
              rsync -Havu /srv/nfs/masters_Donna-Collection/* /srv/masters_donna-collection/
              rsync -Havu /srv/nfs/masters_Dragons-Den/* /srv/masters_dragons-den/
              rsync -Havu /srv/nfs/masters_Koi-Pond/* /srv/masters_koi-pond/
              rsync -Havu /srv/nfs/masters_DVR/* /srv/masters_DVR/'''
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
        sh '''for collection in Koi-Pond Dragons-Den Donna-Collection
        do
        python3 ./loadplexdata.py -i /srv/nfs/masters_${collection}/MakeMKV -o /srv/plexmedia_symlinks/${collection}_TV/ -c ./convertTV.yml
        done'''
      }
    }
    stage('Generate or update symlink catalog of video masters in k8s after restore of backup') {
      agent {
        label "plex-volumes"
      }
      steps {
        echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
        sh '#python3 ./loadplexdata.py -i /srv/masters_DVR/PlayOn -o /srv/plexmedia_symlinks/DVR_TV/ -c ./convertTV.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_Movies/ -c ./convertMovies.yml'
        sh 'python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/PlayOn -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '#python3 ./loadplexdata.py --dvr -i /srv/masters_DVR/temp -o /media/DVR_TV/ -c ./convertTV.yml'
        sh '''for collection in koi-pond rose-garden dragons-den donna-collection roger-roger
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_Movies/ -c ./convertMovies.yml
        done'''
        sh '''for collection in koi-pond dragons-den donna-collection
        do
        python3 ./loadplexdata.py -i /srv/masters_${collection}/MakeMKV -o /media/${collection}_TV/ -c ./convertTV.yml
        done'''
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
