node('jenkins-slave') {
    stage('conan-io-training') {
        sh(script: """
            
            
                
            
            echo "cloning conan-io-training Git"
            mkdir conan-io
            cd conan-io
            git clone https://github.com/conan-io/training.git
            cd training
            cd docker_environment   
            
            podman run dir:./artifactory-training -dt- p 8082:8082/tcp
            podman run dir:./conan-training -dt 
            
            podman exec -it conan-training bash
        """)
    }
}
