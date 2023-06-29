node {
    stage('Build') {
        node {
            docker.image('python:3-alpine').inside {
                sh 'python -m py_compile $(pwd)/sources/add2vals.py $(pwd)/sources/calc.py'
            }
        }
    }
    
    stage('Test') {
        node {
            docker.image('qnib/pytest').inside {
                sh 'py.test --verbose --junit-xml test-reports/results.xml $(pwd)/sources/test_calc.py'
            }
        }
        
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
    }
}
