pipeline {
        agent any
            stages
                {
                stage('Stage 1')
                    {
                    steps {
                        git branch: 'master', url: 'https://github.com/shcoderepo/tenable.git'
                    }
                }
                stage('set virtualenvironment') {
                steps {
                    script {
                            sh '''
                            echo $WORKSPACE
                            echo $PATH
                            set +e
                            export PATH=/usr/local/bin/virtualenv:$PATH
                            export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python
                            export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
                            source /usr/local/bin/virtualenvwrapper.sh
                            rmvirtualenv testproject
                            mkvirtualenv testproject
                            pip install --upgrade pip
                            #pip install -r requirements.txt -r dev-requirements.txt
                            pip install -r requirements.txt
                            make clean
                            '''
                      }
                }
            }
                stage('Setup')
                         { // Install any dependencies you need to perform testing
                            steps {
                                script {
                                        sh """
                                        pip install -r requirements.txt
                                        """
                    }
             }
        }
    }
}
