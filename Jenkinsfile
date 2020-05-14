pipeline {
  agent any
  parameters {
    string(name: 'IMAGENAME')
  }
  }
  stages {
        stage('Docker Bench Mark'){ 
            steps
             { 
                
                echo "EXECUTING DOCKER BENCH SECURITY"
                echo "================================"
                sh 'docker run --net host --pid host --userns host --cap-add audit_control -e DOCKER_CONTENT_TRUST=$DOCKER_CONTENT_TRUST -v /var/lib:/var/lib -v /var/run/docker.sock:/var/run/docker.sock -v /usr/lib/systemd:/usr/lib/systemd -v /etc:/etc --label docker_bench_security docker/docker-bench-security -l /test-log.log' 
                sh 'rm test-log.log'
                sh 'docker cp $(docker ps -aq | head -1):/test-log.log .'
              }  
          post {
            always {
                  archiveArtifacts 'test-log.log'
                   }
            always { 
                   cleanWs()
                   }
                }
            
            }  
    }
 }

