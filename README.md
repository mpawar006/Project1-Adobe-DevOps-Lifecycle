# Abode Software: CI/CD Pipeline Implementation

## 📝 Project Overview

Implemented a robust DevOps lifecycle to automate the company's build, test, and deployment processes. This project utilizes a **Jenkins Pipeline** to orchestrate the workflow, which is triggered by changes in a **GitHub repository**. This solution ensures a streamlined and efficient development and release process, with separate workflows for development and production environments.

---

## 🚀 Pipeline Flow

The CI/CD pipeline is designed to respond to commits on different Git branches, providing a clear distinction between development and production activities.

### Git Workflow
A **Git workflow** is implemented with two primary branches:
- **`develop` branch**: For ongoing development and feature work. Commits to this branch trigger a build and test job.
- **`master` branch**: For stable, production-ready code. Commits to this branch trigger a full build, test, and production deployment.

### Jenkins Pipeline Jobs
The pipeline is composed of the following jobs, defined in a Jenkinsfile:

1.  **`build` Job (Triggered by both `master` and `develop` branches)**:
    - This job is triggered automatically by a commit to either the `master` or `develop` branch on GitHub.
    - It pulls the latest code from the repository.
    - The code is then containerized using a `Dockerfile`, which builds a new image based on the provided base image.
    - The application code is placed in the `/var/www/html` directory inside the container.

2.  **`test` Job (Triggered by both `master` and `develop` branches)**:
    - After the `build` job is successful, this job is executed.
    - It runs a series of automated tests to verify the functionality of the application.
    - If the commit was on the `develop` branch, the pipeline stops here after a successful test.

3.  **`prod` Job (Triggered only by the `master` branch)**:
    - This job is only executed if the `build` and `test` jobs are successful and the commit was on the `master` branch.
    - It pushes the newly built and tested Docker image to a container registry.
    - It then deploys the application to the production environment.

---

## 🛠️ Technologies Used

| Tool/Technology | Role in Project |
| :--- | :--- |
| **Configuration Management Tool** | Used to install necessary software on machines to prepare them for the pipeline (e.g., Jenkins, Docker). |
| **Git** | Version control system for managing the application's source code and enabling the branching strategy. |
| **Jenkins** | CI/CD automation server to orchestrate the entire pipeline with a **Declarative Pipeline Script**. |
| **Docker** | Containerization platform for packaging the application and its dependencies into a portable image. |
| **GitHub** | Repository hosting service to store the code and trigger Jenkins builds. |

---

## ⚙️ How to Use

1.  **Setup Configuration Management**: Ensure the necessary software (Jenkins, Docker, etc.) is installed on your machines using a configuration management tool.
2.  **Jenkins Configuration**:
    - Set up a Jenkins server and install the necessary plugins (e.g., Git Plugin, Docker Pipeline Plugin).
    - Create a new **Declarative Pipeline** job in Jenkins.
    - Configure the pipeline to connect to your GitHub repository and trigger builds on commit.
    - Use the provided `Jenkinsfile` to define the `build`, `test`, and `prod` stages.
3.  **Git Workflow**: Adhere to the defined Git workflow, making commits to the `develop` branch for testing and the `master` branch for production releases.
