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
            sh '''#!/bin/bash
            echo 'Running pytest inside Conda environment'

            # Set Conda Path
            export PATH="/home/karan/miniconda3/bin:$PATH"
            
            # Initialize Conda
            source /home/karan/miniconda3/etc/profile.d/conda.sh || echo "Conda init failed"

            # Verify Conda works
            conda --version || { echo "Conda not found"; exit 1; }

            # Activate the environment
            conda activate mlip || { echo "Environment activation failed"; exit 1; }

            # Run pytest
            pytest --maxfail=5 --disable-warnings
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