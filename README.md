# **Automated CI/CD Pipeline: Flask App Deployment**

This project demonstrates core DevOps principles, including Containerization, CI/CD (Continuous Integration/Continuous Delivery), and secure Pipeline as Code, by automatically building and deploying a Python Flask application on every code commit.

## 🚀 Project Overview
The goal of this project was to establish a fully automated software delivery process. Any change pushed to the main branch automatically triggers a workflow that builds a Docker image and publishes it to Docker Hub.

Technologies Used
|Category|Tool|Purpose|
|:---|:---:|---:|
|Source Control|Git / GitHub|Version control and repository hosting.|
|CI/CD Platform|GitHub Actions|Defined the automated build and push workflow (Pipeline as Code).|
|Containerization|Docker|Packaged the application and dependencies into a single, portable image.|
|Registry|Docker Hub|Remote repository for storing the final Docker image.|
|Application|Python 3 / Flask|Simple "Hello World" web application.|

## 🏗️ Architecture and Flow
The pipeline uses GitHub Actions to orchestrate the build and push process.

1. **Code Commit**: Developer pushes code to the main branch.

2. **Workflow Trigger**: GitHub Actions detects the push and starts the pipeline defined in .github/workflows/deploy.yml.

3. **Authentication**: The pipeline securely logs into Docker Hub using encrypted GitHub Secrets.

4. **Build**: A Docker image is built using the provided Dockerfile.

5. **Push**: The resulting Docker image is tagged (with latest and a unique commit SHA) and pushed to the public Docker Hub repository.

6. **Verification**: The new image is immediately available for deployment on any target environment.

## 📋 Setup and Execution
To replicate this project or run the application locally, follow these steps.

**Prerequisites**
You need the following installed locally:

* Git

* Docker

* A Docker Hub Account (for the push step)

##**Step 1: Local Setup and Containerization**
1. **Clone the Repository:**
```bash
git clone [YOUR-REPO-URL]
cd [your-repo-name]
```

2. **Build the Docker Image Locally:**

```bash
docker build -t devops-classic-app:local .
```

3. **Run the Container Locally (Test):**

```bash
docker run -d -p 8080:5000 --name my-test-app devops-classic-app:local
```

Access the application at http://localhost:8080/.

## **Step 2: Configure the CI/CD Pipeline (GitHub Actions)**
The pipeline is defined in the file: .github/workflows/deploy.yml.

1. **Create Secrets**: The workflow requires three GitHub Secrets to authenticate with Docker Hub. Navigate to Settings → Secrets and variables → Actions in your GitHub repository and create these variables:

|Secret Name|Purpose|
|DOCKER_USERNAME|Your Docker Hub Username|
|DOCKER_PASSWORD|Your Docker Hub Personal Access Token (PAT)|
|IMAGE_NAME|The full Docker Hub path (e.g., yourusername/devops-classic-app)|

2. **Trigger the Pipeline**: Ensure your Dockerfile, app.py, requirements.txt, and .github/workflows/deploy.yml are all committed and pushed to the main branch. This will automatically trigger the CI/CD workflow.

3. **Monitor**: Check the Actions tab on the GitHub repository to monitor the build, login, and push status.

## 📁 Repository Contents
|File/Folder|Description|
|app.py|The main Python Flask application file.|
|requirements.txt|Lists the Python dependencies (Flask).|
|Dockerfile|Instructions for building the container image.|
|.github/workflows/|Contains the YAML file defining the CI/CD workflow.|
|deploy.sh|(Optional) Simple Bash script used for initial local deployment testing.|

## 💡 Key DevOps Learning Outcomes
* **Security Best Practices**: Secured sensitive credentials (Docker Hub PAT) using environment-specific secrets (DOCKER_PASSWORD) rather than hard-coding them.

* **Pipeline as Code**: Managed the entire build, test, and push process using declarative YAML syntax.

* **Immutability**: Images are built once and promoted, ensuring the artifact tested is the same one deployed.

* **Containerization**: Demonstrated proficiency in packaging applications for portability and consistency.
