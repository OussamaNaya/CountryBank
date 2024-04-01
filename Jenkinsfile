pipeline {
  // Use a specific agent with tools installed (replace 'docker' with your agent name)
  agent any

  stages {
    stage('Git Checkout') {
      steps {
        // Fetch code from your Git repository
        git 'https://github.com/jaiswaladi246/CountryBank.git'
      }
    }

    stage('OWASP Dependency Check') {
      steps {
        // Perform dependency check with additional arguments (adjust path if needed)
        dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DC'
        // Publish dependency check report
        dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
      }
    }

    stage('Trivy') {
      steps {
        // Define the PATH environment variable within the script (assuming Trivy is in user's Documents)
        bat '''
               C:\\Users\\user\\Documents\\trivy\\trivy.exe fs .
            '''
      }
    }

    stage('Build & deploy') {
      steps {
        // Check if nohup is available (optional)
        sh 'where nohup'
        // Build and deploy using docker-compose (replace command if needed)
        sh "docker-compose up -d"
      }
    }
  }
}
