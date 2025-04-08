pipeline{
    
    agent any
    
    triggers{
        githubPush()
    }
    
    environment{
        PATH = "C:/Program Files/Docker/Docker/resources/bin/"
        IMAGE_NAME = "ymg-sinav-image"
        CONTAINER_NAME = "ymg-sinav-container"
    }    

    stages{
        stage('Repoyu Klonla'){
            steps{
                echo "Repo Klonlandı!"
                git url:'https://github.com/yakupyigittek/ymgsinav.git', branch: 'main'
            }
        }
        
        stage('Docker Image Oluştur'){
            steps{ 
                echo "Docker Image Oluşturuldu!"
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }
        
        stage('Eski Containeri Durdur'){
            steps{
                echo "Eski Container Durduruldu!"
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        
        stage('Yeni Conteyneri Oluştur'){
            steps{
                echo "Yeni Container Oluşturuldu!"
                sh "docker run -d --name ${CONTAINER_NAME} -p 5050:80 ${IMAGE_NAME}"
            }
        }
    }
    
    post{
        success{
            echo "Yayın başarılı"
        }
        
        failure{
            echo "Pipeline başarısız oldu"
        }
    }
    
}