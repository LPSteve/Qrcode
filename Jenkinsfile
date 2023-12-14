node ('qrcode') {
    def app
    stage('Cloning Git') {
        /* Making sure repository is cloned to workspace*/
       checkout scm
    } 

    stage('Build-and-Tag') {
        /* This builds the image. Synonymous to docker build command in CLI in app server*/
        app = docker.build("lopdave/qrcode")
    }

    stage('Post-to-dockerhub') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push("latest")
        }
    }

    stage('Pull-image-server') {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}
