pipeline {
    agent any

    stages {
        stage('Clone sources') {
            steps {
                git credentialsId: 'jenkins-ssh',
                    url: 'git@github.com:v3rtumnus/jekyll-blog.git'
            }
        }

        stage('Build blog site') {
            steps {
                withEnv(['PATH+EXTRA=/var/lib/jenkins/gems/bin', 'GEM_HOME=/var/lib/jenkins/gems']) {
                  sh 'bundle install'
                }
            }
        }

        stage('Deploy to apache') {
            steps {
                withEnv(['PATH+EXTRA=/var/lib/jenkins/gems/bin', 'GEM_HOME=/var/lib/jenkins/gems']) {
                  sh 'JEKYLL_ENV=production jekyll build -d /var/www/html'
                }
            }
        }
    }
}
