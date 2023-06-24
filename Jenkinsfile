node {
    withDockerContainer('python:2-alpine') {
        // some block
        stage('Build') {
            checkout scm
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
	withDockerContainer('qnib/pytest') {
        // some block
        stage('Test') {
            checkout scm
            sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            junit 'test-reports/results.xml'
        }
    }
    withDockerContainer('cdrx/pyinstaller-linux:python2') {
        // some block
        stage('Deploy') {
	    input message: 'lanjutkan ke tahap deploy?'
            checkout scm
            sh 'pyinstaller --onefile sources/add2vals.py'
            archiveArtifacts artifacts: 'sources/add2vals.py', followSymlinks: false
        }
    }
}
