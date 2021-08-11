# bk-volumes-docker-jenkins
PIpeline en jenkins para automatizar bk de volumenes con script .sh escrito en python

# Pipeline 


pipeline {
    
    
    gent {label'miserver'}
     environment{
        fichero = fileExists file: "/home/randi/Desktop/data231.tar" 
 }
 
    stages {

        stage ("eliminar bk antiguo"){
            when{expression {fichero=='true'}}
            steps{ 
                sh 'rm -R $ruta/home/randi/Desktop/data231.tar'
            }
        }
              //Detener contedor para sacar bk al volumen
        stage ("detener docker"){
            steps{ 
                sh 'docker stop data23'
            }
        }
    
        
        stage ("ejecucion del script "){
            steps{ 
                sh './docker-volumes.sh data23 save /home/randi/Desktop/data231.tar'
            }
        }
       stage ("Iniciar Docker" ){
             steps{ 
                sh 'docker start data23'
            }
        }
    }
        
}
