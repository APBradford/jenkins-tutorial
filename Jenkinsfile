pipeline{
        agent any
        stages{
            stage('Clone Directory'){
                steps{
                    sh "git clone https://gitlab.com/qacdevops/chaperootodo_client.git"
                }
            }
            stage('Install Docker and Docker-Compose'){
                steps{
                    sh "sudo apt install -y curl jq"
                    sh "curl https://get.docker.com | sudo bash"
                    sh "version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name')"
                    sh "sudo curl -L "https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose"
                    sh "sudo chmod +x /usr/local/bin/docker-compose"
                }
            }
            stage('Deploy App'){
                steps{
                    sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d."
            }
        }
}
