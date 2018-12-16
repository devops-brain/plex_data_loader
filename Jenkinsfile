node {
  // Pull code from repo?
  // stage 'Stage Checkout'
  // checkout scm

  // Copy TV Shows
  stage 'Copy TV'
  sh 'for collection in Dragons_Den Koi_Pond; do python3 /usr/local/bin/loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plex/${collection}/TV/ -c /etc/loadplexdata/convertTV.yml; done'

  // Copy Movies
  stage 'Copy Movies'
  sh 'for collection in Roger_Roger Rose_Garden Donna_Collection Dragons_Den Koi_Pond; do python3 /usr/local/bin/loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plex/${collection}/Movies/ -c /etc/loadplexdata/convertMovies.yml; done'

  // Copy Movies from DVR2
  stage 'Copy Movies Playon'
  sh 'python3 /usr/local/bin/loadplexdata.py -i /srv/masters/Koi_Pond/PlayOn -o /srv/plex/DVR/Movies/ -c /etc/loadplexdata/convertMovies.yml'

  // Copy TV from DVR2
  stage 'Copy TV Playon'
  sh 'echo "TODO"'
}
