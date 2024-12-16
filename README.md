# CI/CD Pipeline for AWS Lambda and Terraform Infrastructure Deployment

## Project Overview
This project automates the deployment of an AWS Lambda function and associated infrastructure using Terraform. The pipeline is implemented in GitHub Actions and follows a structured CI/CD approach with Source, Build, and Deploy stages.

### Key Features:
- Validates Lambda function source code and Terraform configurations.
- Builds and packages the Lambda function for deployment.
- Deploys the Lambda function and infrastructure to AWS using Terraform.

---

## Directory Structure
```plaintext
├── terraform/
│   ├── main.tf            # Terraform configuration for AWS resources
│   ├── provider.tf        # AWS provider setup
│   ├── variables.tf       # Terraform variables definition
│   ├── vars.tfvars        # Variable values for the Terraform script
├── lambda/
│   ├── handler.js         # Lambda function code
│   ├── package.json       # Node.js project configuration 
├── src/
│   ├── app.js.tpl         # Template file for the `app.js` script
│   ├── index.html         # Main HTML file for the static website
│   ├── styles.css         # Contains the CSS styles for the static website
├── .github/
│   ├── workflows/
│       ├── main.yml  # GitHub Actions workflow definition
├── README.md              # Project documentation
```

---

## Prerequisites
1. **AWS Account** with programmatic access.
   - Set up IAM credentials and store them as GitHub Secrets:
     - `AWS_ACCESS_KEY_ID`
     - `AWS_SECRET_ACCESS_KEY`
2. **Terraform Installed**: Ensure Terraform is installed locally for validation purposes.
3. **Node.js Installed**: Required for running and testing the Lambda function locally.
4. **GitHub Repository**: This project assumes the code is hosted in a GitHub repository.

---

## Pipeline Stages
The GitHub Actions workflow is divided into three main stages:

### 1. **Source Stage**
- Validates the Terraform configuration using `terraform validate`.
- Lints the Lambda source code using `npm run lint` (requires a linting configuration in `package.json`).

### 2. **Build Stage**
- Installs Node.js dependencies for the Lambda function.
- Packages the Lambda function into a `.zip` file.
- Uploads the `.zip` file as an artifact for the Deploy stage.
- Validates the Terraform plan using `terraform plan`.

### 3. **Deploy Stage**
- Downloads the packaged Lambda `.zip` file.
- Applies the Terraform configuration to deploy infrastructure.
- Deploys the Lambda function to AWS using the AWS CLI.

---

## Deployment Instructions

### Step 1: Clone the Repository
```bash
git clone https://github.com/darshanrw/CICD_FinalProject.git
cd CICD_FinalProject
```

### Step 2: Install Dependencies
Navigate to the Lambda directory and install Node.js dependencies:
```bash
cd lambda
npm install
```

### Step 3: Configure Terraform Variables
Update the `terraform/vars.tfvars` file with your desired configurations, such as resource names and regions.

### Step 4: Push Changes to GitHub
Ensure your code is committed and pushed to the `main` branch:
```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### Step 5: Monitor the Workflow
- Navigate to your GitHub repository.
- Go to **Actions** and monitor the CI/CD pipeline.

---

## Usage
Once the pipeline completes successfully:
- The infrastructure (e.g., Lambda, S3, etc.) will be provisioned on AWS.
- The Lambda function will be deployed and updated with the latest code.

You can test the Lambda function using the AWS Console or CLI:
```bash
aws lambda invoke --function-name <Function-name> --region us-east-1 output.json
cat output.json
```

---

## Troubleshooting
### Common Issues:
1. **Terraform Initialization Error**:
   - Ensure your AWS credentials are correctly configured in GitHub Secrets.
2. **Dependency Issues**:
   - Run `npm install` to resolve any missing dependencies.
3. **Terraform Plan Fails**:
   - Check the Terraform configuration files for syntax or logical errors.

---

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature
   ```
3. Commit your changes and push to your fork.
4. Submit a pull request.

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

---

## Contact
For questions or support, reach out to:
- **Name**: Darshan Wadekar
- **Email**: [wadekar.darshan04@gmail.com]
- **GitHub**: [darshanrw](https://github.com/darshanrw)
