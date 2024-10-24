## DEPI graduation project
# Project Pipeline for nhorizon-java-container

## Process Overview

1. **Cloning the Repository**
   - The `nhorizon-java-container` repository was cloned to the local machine using Git, providing access to all project files.

2. **Modifying the Front Page**
   - The `views` directory was accessed, and the `home.pug` file was opened.
   - The file was modified to prominently display the group code on the front page.

3. **Creating the Jenkinsfile**
   - A new file named `Jenkinsfile` was created in the root of the repository.
   - The Jenkinsfile was structured as a declarative pipeline, including the following stages:
     - Building a new Docker image with the updated application files.
     - Pushing the Docker image to the public Docker Hub account.
     - Pulling the image on another Jenkins agent to ensure accessibility.
     - Running the image on the agent to start the application.
     - Checking the connectivity of the deployed application to confirm accessibility.

4. **Setting Up Jenkins**
   - Jenkins was ensured to be installed and configured on the server.
   - A new pipeline job was created in Jenkins and linked to the cloned GitHub repository.

5. **Running the Pipeline**
   - The pipeline was triggered in Jenkins, and the console output was monitored for any issues during execution.

6. **Verifying the Deployment**
   - Upon successful completion of the pipeline, the application was accessed in a web browser to verify that it was running correctly.

  ![Pipeline Diagram](https://drive.google.com/file/d/1t0fVbMFqw9tsC2oGs0GYBWtkm-CUyrKr/view?usp=sharing)

### Common Challenges Encountered

#### 1. **Resource Limitations with Virtual Machines (VMs)**
   Due to resource constraints on Virtual Machines, we had to switch to using a combination of Windows
    Subsystem for Linux (WSL) and Windows which uses less resources while maintaining a compatible development environment.

#### 2. **Manual Copying of SSH Keys**
   When copying SSH keys manually, be cautious of hidden characters like `\n` (newline). 
   These can be easily missed and may cause issues during the authentication process.

#### 3. **Jenkins Environment Variable Differences Between Linux and Windows**
   There are syntax differences when using environment variables in Jenkins depending on the operating system. 
   Below are examples of how to handle them:

   - **Linux (Bash):**
     ```bash
     sh "docker push $DOCKER_IMAGE"
     ```

   - **Windows (Batch):**
     ```bat
     bat 'docker pull %DOCKER_IMAGE%'
     ```

   Make sure to adjust environment variable syntax based on the agent’s operating system to ensure compatibility.
