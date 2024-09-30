node('agent1') {
    def app // Объявляем переменную

    stage('Cloning Git') {
        checkout scm
    }

    stage('Build-and-Tag') {
        app = docker.build("traktori/timp1") // Строим и присваиваем переменной app
    }

    stage('Post-to-dockerhub') {
        docker.withRegistry('traktori', 'timp1') {
            app.push("latest") // Пушим с тэгом "latest"
        }
    }

    stage('Pull-image-server') {
        sh "docker-compose down" // Останавливаем контейнеры
        sh "docker-compose up -d" // Запускаем контейнеры в фоновом режиме
    }
}
