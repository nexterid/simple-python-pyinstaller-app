node {
    withDockerContainer('python:2-alpine') {
        // some block
        stage('Build') {
            checkout scm
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
}
