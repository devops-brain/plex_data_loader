Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any

    stages {
        stage('MakeMKV TV') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'for collection in Dragons_Den Koi_Pond; do python3 /usr/local/bin/loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plex/${collection}/TV/ -c /etc/loadplexdata/convertTV.yml; done'
            }
        }
        stage('MakeMKV Movies') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'for collection in Roger_Roger Rose_Garden Donna_Collection Dragons_Den Koi_Pond; do python3 /usr/local/bin/loadplexdata.py -i /srv/masters/${collection}/MakeMKV -o /srv/plex/${collection}/Movies/ -c /etc/loadplexdata/convertMovies.yml; done'
            }
        }
        stage('PlayOn TV') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo 'TODO'
            }
        }
        stage('PlayOn Movies') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                sh 'python3 /usr/local/bin/loadplexdata.py -i /srv/masters/Koi_Pond/PlayOn -o /srv/plex/DVR/Movies/ -c /etc/loadplexdata/convertMovies.yml'
            }
        }
    }
}
