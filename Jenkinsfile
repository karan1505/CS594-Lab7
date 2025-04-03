pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                echo 'In C or Java, we can compile our program in this step'
                echo 'In Python, we can build our package here or skip this step'
                '''
            }
        }
        
        stage('Test') {
            steps {
                sh '''#!/bin/bash -l
                echo 'Running pytest inside Conda environment'

                # Set Conda Path
                export PATH="/home/karan/miniconda3/bin:$PATH"
                
                # Initialize Conda properly
                eval "$(conda shell.bash hook)"

                # Activate the Conda environment
                conda activate mlip || {
                    echo "Environment activation failed"; exit 1;
                }

                # Verify Python and pytest are available
                python --version || {
                    echo "Python not found in environment"; exit 1;
                }
                pytest --version || {
                    echo "pytest not found, ensure it is installed in mlip"; exit 1;
                }

                # Run pytest
                pytest --maxfail=5 --disable-warnings || {
                    echo "Tests failed"; exit 1;
                }
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'In this step, we deploy our project'
                echo 'Depending on the context, we may publish the project artifact or upload pickle files'
            }
        }
    }
}
