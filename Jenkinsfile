pipeline {
    agent {
        docker { image 'ubuntu'
        args '-u root:root'
        }
    }
    stages {
        stage('Clone') {
            steps {
                git branch:'master',url:'https://github.com/EnriquePM/ic-diccionario.git'
            }
        }
        stage('Install') {
            steps {
                sh 'apt-get update && apt-get install -y aspell-es ' 
            }
        }
        stage('Test')
        {
            steps {
                sh '''
                export LC_ALL=C.UTF-8
                OUTPUT=`cat doc/*.md | aspell list -d es -p ./.aspell.es.pws`; if [ -n "$OUTPUT" ]; then echo $OUTPUT; exit 1; fi'''
            }
        }
    }
}
