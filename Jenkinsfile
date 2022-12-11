pipeline{
    agent {label 'DOCKER'}
    environment{
        dockerhub=credentials('dockerid')
    }
    stages{
        stage('pulling from scm'){
            steps{
                git url:'https://github.com/DevprojectsForDevOps/StudentCoursesRestAPI',
                branch: 'master'
            }
        }
        stage('build image'){
            steps{
                sh 'docker image build -t studentcoursesrestapi:1.0 .'
            }
        }
        stage('pushing image into docker hub '){
            steps{
                sh 'docker tag studentcoursesrestapi:1.0 nagvenkat/studentcoursesrestapi:1.0'
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
                sh 'docker push nagvenkat/studentcoursesrestapi:1.0'
                
            }
        }
		stage('Run container'){
            steps{
                sh 'docker container run --name scr -d -p 8082:8080 nagvenkat/studentcoursesrestapi:1.0'
            }
        }
    }
}
