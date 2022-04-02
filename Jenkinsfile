node('jenkins-slave') {
    stage('conan-io-training') {
        sh(script: """
            
            curl -o /usr/local/bin/podman-compose https://raw.githubusercontent.com/containers/podman-compose/devel/podman_compose.py \
                && chmod +x /usr/local/bin/podman-compose
                
            podman-compose version
            echo "cloning conan-io-training Git"
            mkdir conan-io
            cd conan-io
            git clone https://github.com/conan-io/training.git
            cd training
            cd docker_environment   
            podman-compose up -d
            podman exec -it conan-training bash
        """)
    }
}
