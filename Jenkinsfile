node('jenkins-slave') {
    stage('conan-io-training') {
        sh(script: """
            
            
            podman version
            echo "cloning conan-io-training Git"
            mkdir conan-io
            cd conan-io
            git clone https://github.com/conan-io/training.git
            cd training
            cd docker_environment            
            podman run -dt
            podman exec -it conan-training bash
        """)
    }
}