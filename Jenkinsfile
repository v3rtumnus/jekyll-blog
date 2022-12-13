pipeline {
    agent any

    stages {
        stage('Clone sources') {
            steps {
                git credentialsId: 'github-ssh',
                    url: 'git@github.com:v3rtumnus/jekyll-blog.git'
            }
        }

        stage('Build blog site') {
            steps {
                withEnv(['PATH+EXTRA=/var/jenkins_home/gems/bin', 'GEM_HOME=/var/jenkins_home/gems']) {
                  sh 'bundle install'
                }
            }
        }

        stage('Deploy to apache') {
            steps {
                withEnv(['PATH+EXTRA=/var/jenkins_home/gems/bin', 'GEM_HOME=/var/jenkins_home/gems']) {
                  sh 'JEKYLL_ENV=production jekyll build -d /var/www/html'
                }
            }
        }
    }
}
