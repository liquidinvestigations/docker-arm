// vim: ft=groovy

node('arm64') {
  parallel(
    hoover_search: {
      node('arm64') {
        deleteDir()
        checkout scm
        stage('Prepare a Factory') {
          sh 'git clone https://github.com/liquidinvestigations/factory'
          sh 'cd factory/images; mkdir cloud-arm64; cd cloud-arm64; curl -L https://jenkins.liquiddemo.org/__images__/factory/cloud-arm64-image.tar.xz | xzcat | tar x'
        }
        stage('Build Docker image') {
          def TARGET = 'hoover-search'
          sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm time /mnt/docker-arm/build $TARGET /mnt/docker-arm/$TARGET.dockers'
        }
        stage('Archive artifacts') {
          archiveArtifacts TARGET + '.dockers'
        }
      }
    },
    hoover_snoop: {
      node('arm64') {
        deleteDir()
        checkout scm
        stage('Prepare a Factory') {
          sh 'git clone https://github.com/liquidinvestigations/factory'
          sh 'cd factory/images; mkdir cloud-arm64; cd cloud-arm64; curl -L https://jenkins.liquiddemo.org/__images__/factory/cloud-arm64-image.tar.xz | xzcat | tar x'
        }
        stage('Build Docker image') {
          def TARGET = 'hoover-snoop'
          sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm time /mnt/docker-arm/build $TARGET /mnt/docker-arm/$TARGET.dockers'
        }
        stage('Archive artifacts') {
          archiveArtifacts TARGET + '.dockers'
        }
      }
    },
    hoover_ui: {
      node('arm64') {
        deleteDir()
        checkout scm
        stage('Prepare a Factory') {
          sh 'git clone https://github.com/liquidinvestigations/factory'
          sh 'cd factory/images; mkdir cloud-arm64; cd cloud-arm64; curl -L https://jenkins.liquiddemo.org/__images__/factory/cloud-arm64-image.tar.xz | xzcat | tar x'
        }
        stage('Build Docker image') {
          def TARGET = 'elasticsearch'
          sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm time /mnt/docker-arm/build $TARGET /mnt/docker-arm/$TARGET.dockers'
        }
        stage('Archive artifacts') {
          archiveArtifacts TARGET + '.dockers'
        }
      }
    },
    elasticsearch: {
      node('arm64') {
        deleteDir()
        checkout scm
        stage('Prepare a Factory') {
          sh 'git clone https://github.com/liquidinvestigations/factory'
          sh 'cd factory/images; mkdir cloud-arm64; cd cloud-arm64; curl -L https://jenkins.liquiddemo.org/__images__/factory/cloud-arm64-image.tar.xz | xzcat | tar x'
        }
        stage('Build Docker image') {
          def TARGET = 'hoover-ui'
          sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm time /mnt/docker-arm/build $TARGET /mnt/docker-arm/$TARGET.dockers'
        }
        stage('Archive artifacts') {
          archiveArtifacts TARGET + '.dockers'
        }
      }
    },
    tika: {
      node('arm64') {
        deleteDir()
        checkout scm
        stage('Prepare a Factory') {
          sh 'git clone https://github.com/liquidinvestigations/factory'
          sh 'cd factory/images; mkdir cloud-arm64; cd cloud-arm64; curl -L https://jenkins.liquiddemo.org/__images__/factory/cloud-arm64-image.tar.xz | xzcat | tar x'
        }
        stage('Build Docker image') {
          def TARGET = 'tika'
          sh 'factory/factory run --smp 2 --memory 1024 --share .:/mnt/docker-arm time /mnt/docker-arm/build $TARGET /mnt/docker-arm/$TARGET.dockers'
        }
        stage('Archive artifacts') {
          archiveArtifacts TARGET + '.dockers'
        }
      }
    }
  )
}
