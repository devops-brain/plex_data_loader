pipeline {
    agent any

    stages {
        stage('MakeMKV TV') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'for collection in Dragons_Den Koi_Pond; do python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/TV/ -c ./convertTV.yml; done'
            }
        }
        stage('MakeMKV Movies') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'for collection in Roger_Roger Rose_Garden Donna_Collection Dragons_Den Koi_Pond; do python3 ./loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plexmedia/${collection}/Movies/ -c ./convertMovies.yml; done'
            }
        }
        stage('PlayOn TV') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh "for show in ${ls -1 /srv/masters/Koi_Pond/PlayOn | grep -v Netflix | grep -v Hulu | grep -v 'Amazon Prime Video'} do rsync -Havu /srv/masters/Koi_Pond/PlayOn/$(show) /srv/plexmedia/DVR/TV/; done"
            }
        }
        stage('PlayOn Movies') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'python3 ./loadplexdata.py -i /srv/masters/Koi_Pond/PlayOn -o /srv/plexmedia/DVR/Movies/ -c ./convertMovies.yml'
            }
        }
    }
}
