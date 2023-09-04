pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Realiza o checkout do repositório
                    checkout scm
                }
            }
        }

        stage('Build and Run Docker Image') {
            steps {
                script {
                    def image_name = "projetoapi:lts"
                    def container_name = "projetoapi"

                    // Remove o contêiner se existir
                    sh "/usr/bin/docker ps -a | grep $container_name && docker stop $container_name && docker rm $container_name"

                    // Remove a imagem se existir
                    sh "/usr/bin/docker images | grep $image_name && docker rmi $image_name"

                    echo "Construindo imagem: $image_name"
                    sh "/usr/bin/docker build -t $image_name ."

                    echo "Iniciando contêiner: $container_name"
                    sh "/usr/bin/docker run -d --name $container_name -p 80:80 $image_name"
                }
            }
        }
    }
}
