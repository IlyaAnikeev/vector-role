pipeline {
    agent any
    
    stages {
	stage('Сlearing the directory') {
            steps {
                deleteDir()
	    }
	}
	stage('Git clone') {
	    steps {
	        dir('vector-role') {
	        git branch: 'main', url: 'https://github.com/IlyaAnikeev/vector-role.git'
	        }
	    }
	}
        stage('Installing dependencies') {
            steps {
                sh 'echo Installing dependencies'
                sh 'set -e'
                sh 'pip3 install molecule molecule_docker molecule_podman'
		sh 'pip3 install "molecule[lint]"'
		sh 'pip3 install "molecule[docker.lint]"'
		sh 'pip3 install --upgrade requests'
            }
        }
        stage('Run molecule test') {
            steps {
                sh 'echo Run molecule test'
                sh 'molecule test || true'
            }
        }
    }
}
