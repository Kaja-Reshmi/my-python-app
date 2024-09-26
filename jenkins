pipeline{
    agent any

    environment {
          PYTHON_ENV= 'venv'          // Virtual environment for python
    }

stages {
   // stage 1: clone the repository
   stage('checkout'){
       steps {
           echo 'cloning repository...'
           git branch: 'main', url: 'https://github.com/Kaja-Reshmi/my-python-app.git'
    }
// stage 2: set up the python environment
stage('set up environment'){
    steps {
         echo 'setting up python virtual environment...'
         sh'''
             python3 -m venv ${PYTHON_ENV}  #create a virtual environment
             source ${PYTHON_ENV}/Bin/activate   #activate the virtual environment
             pip install -r  requirments.txt   #install dependencies
         '''
    }
 }
//stage 3: Run unite tests
stage('Run Tests') {
    steps {
        echo 'Running unit tests....'
         sh'''
             source ${PYTHON_ENV}/bin/activate       #ACTIVATE THE VIRTUAL ENVIRONMENT 
             pytest tests/                           #run the unit test using pytest
        '''
  }
}
//stage 4: Deploy(this could be to a local HTTP server, for example)
stage('Deploy'){
    steps {
        echo 'Deploying applications...'
        //In this example, we,ll simulate deployment by copying the code to a server directory
        sh'''
          cp -r * /path/to/local/http/server/root/  #copy the app to the deployment directory
        '''
    }
}
}
post{
   always {
      echo 'cleaning up workspace...'
       cleanWs()
}
 success {
echo 'pipeline completed successfully!'
}
failure {
  echo 'pipeline failed!'
}
}
