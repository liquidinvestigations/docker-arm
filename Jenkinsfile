// vim: ft=groovy
node('arm64') {
    deleteDir()
    checkout scm
    stage('Build a Factory') {
        sh 'git clone https://github.com/liquidinvestigations/factory'
    }
    stage('Prepare cloud image') {
        sh 'factory/factory prepare-cloud-image'
    }
    stage('Build Docker image') {
        sh 'mkdir images'
        sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm --share images:/mnt/images time /mnt/docker-arm/build $TARGET'
    }
    stage('Archive artifacts') {
        def TARGET = System.getEnv('TARGET')
        def image = 'images/' + TARGET + '.dockers'
        archiveArtifacts image
    }
}
