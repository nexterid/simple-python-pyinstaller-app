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
	stage('Deploy') {
        // some block
        input message: 'lanjutkan ke tahap deploy?'
        checkout scm
        sh 'docker run --rm -v /home/dicoding/jenkins/submission/simple-python-pyinstaller-app/sources:/src cdrx/pyinstaller-linux:python2 \'pyinstaller -F add2vals.py\''
        archiveArtifacts artifacts: 'sources/add2vals.py', followSymlinks: false
        sh 'docker run --rm -v /home/dicoding/jenkins/submission/simple-python-pyinstaller-app/sources:/src cdrx/pyinstaller-linux:python2 \'rm -rf build dist\''
        sleep time: 1, unit: 'MINUTES'
    }
}
