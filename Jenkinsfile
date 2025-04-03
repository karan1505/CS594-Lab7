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

                # Ensure Conda is available
                export PATH="/home/karan/miniconda3/bin:$PATH"
                source /home/karan/miniconda3/etc/profile.d/conda.sh

                # Activate Conda environment
                conda activate mlip || { echo "❌ Environment activation failed"; exit 1; }

                # Check Python & pytest versions
                python --version || { echo "❌ Python not found in environment"; exit 1; }
                pytest --version || { echo "❌ pytest not installed"; exit 1; }

                # Run tests
                echo "✅ Running pytest..."
                pytest --maxfail=5 --disable-warnings || { echo "❌ Tests failed"; exit 1; }
                echo "✅ All tests passed!"
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
