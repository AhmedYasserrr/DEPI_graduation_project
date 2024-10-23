## DEPI graduation project
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
