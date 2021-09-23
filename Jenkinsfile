pipeline{
    
    agent any
    tools {
        maven "maven-3.8.2"
    }
    parameters{
        string(name:'OPERATION', defaultValue:'package', description: 'Operación maven a realizar')
        string(name:'REPO_URL', defaultValue:'https://github.com/ddieza04/jenkinspipeline.git', description: 'Url del repositorio Git')        
    }
    stages{
        stage("Verificación"){
            steps {
                sh "java -version"
                sh "mvn -version"
                echo "Operación a ejecutar: ${params.OPERATION}"
            }
        }

        stage ("Descarga del código y build") {
            steps {
                git "${params.REPO_URL}"
                sh "mvn clean ${params.OPERATION}"
            }
        }
    }
    
    post{
        success{
            junit 'target/surefire-reports/TEST-*.xml'
        }
    }
}
