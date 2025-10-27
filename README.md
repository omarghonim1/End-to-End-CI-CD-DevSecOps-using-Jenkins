This project is configured to run fully through Jenkins. All required tools and steps are defined in the `Jenkinsfile`. The Jenkins setup includes:
> All build, test, and deployment steps are automated in the `Jenkinsfile`.

## Project Architecture

This project follows a full CI/CD pipeline with the following stages:

1. **Source Code**  
   - Developers push code to the repository.

2. **Security Checks**  
   - Code quality and security scans are performed using **SonarQube** and **OWASP rules**.
   
3. **Integration & Packaging**  
   - The application is packaged into a **Docker image**.
   - The image is pushed and stored in **Docker Hub**.

4. **Deployment**  
   - Jenkins server handles deployment.
   - The application is automatically started after each release.

### Success Criteria
- CI/CD pipeline passes all **quality gates** and **scans**.
- Docker image is successfully **pushed to Docker Hub**.
- Application is successfully **deployed to the target server**.
- Users can **access the application UI**, **add items**, **test app functionality**, and **create new users**.

<img width="1790" height="1013" alt="Screenshot 2025-10-26 171056" src="https://github.com/user-attachments/assets/d0efa0bb-0353-4c4c-8643-be996bc7f240" />

- **Plugins**: Recommended plugins for this project
<img width="1105" height="875" alt="Screenshot 2025-10-26 173107" src="https://github.com/user-attachments/assets/b2f1aec5-6817-4c7f-9203-0fadedffc061" />

- **Tools installed via Jenkins**:
  - SonarQube
    <img width="1547" height="413" alt="Screenshot 2025-10-26 173626" src="https://github.com/user-attachments/assets/91dc2ea8-f857-4051-91d8-3e11b52d72a4" />
  - JDK 11
    <img width="1543" height="377" alt="Screenshot 2025-10-26 173643" src="https://github.com/user-attachments/assets/4a1238d4-f4f5-4f57-8a0c-a1573897dd41" />
  - Maven
    <img width="1327" height="403" alt="Screenshot 2025-10-26 173655" src="https://github.com/user-attachments/assets/e5cf70e2-f18a-4a11-93f6-42ffa577b0e0" />
  - Docker
    <img width="1354" height="397" alt="Screenshot 2025-10-26 173907" src="https://github.com/user-attachments/assets/1c6268b4-5280-4d8c-bdfb-1a8ac1d044b5" />
  - Dependency-Check
<img width="1794" height="319" alt="Screenshot 2025-10-26 174745" src="https://github.com/user-attachments/assets/8991f869-460a-4de9-87fa-89b83c8e6dca" />


**Security Checks (OWASP Scan)**  
   - Performed OWASP security scans on the application source code.  
   - Saved the generated **OWASP scan reports** in the Jenkins pipeline workspace for reference and auditing.
<img width="620" height="251" alt="Screenshot 2025-10-27 154210" src="https://github.com/user-attachments/assets/a2795a9b-f458-48f9-91c8-f32ba53a2469" />

**Docker Installation & Permissions**  
   - Installed Docker on the Jenkins server.  
   - Added the `jenkins` user to the `docker` group to allow Jenkins to run Docker commands.
<img width="764" height="226" alt="Screenshot 2025-10-27 154302" src="https://github.com/user-attachments/assets/c09e2b06-f8d3-4258-b15c-06f0d2746b0f" />

**SonarQube Setup**  
   - Run SonarQube in a Docker container.
       <img width="699" height="234" alt="Screenshot 2025-10-27 154351" src="https://github.com/user-attachments/assets/984d6f5f-99a0-49eb-b009-cd1d2a804305" />
   - Generated a **token** in SonarQube and added it to Jenkins credentials.
     <img width="923" height="282" alt="Screenshot 2025-10-27 154407" src="https://github.com/user-attachments/assets/84029e5e-d772-43f8-9422-a869b1f66925" />
   - Add SonarQube Token in Jenkins
     <img width="1714" height="64" alt="Screenshot 2025-10-27 154509" src="https://github.com/user-attachments/assets/320fb80b-25c8-4749-8039-eecfb278006f" />
   - Defined the SonarQube server inside Jenkins.
     <img width="1281" height="499" alt="Screenshot 2025-10-27 154528" src="https://github.com/user-attachments/assets/76b6674b-1997-430e-bf75-7c9375396590" />

**Code Quality Checks**  
   - Performed code scans on SonarQube.  
   - Code passed the quality checks successfully.
<img width="1477" height="379" alt="Screenshot 2025-10-27 123259" src="https://github.com/user-attachments/assets/aa1e4e51-d7a5-4dd2-91f0-3e1eb0537b2a" />


**Build & Dockerization**  
   - Built a **Docker image** of the application to containerize it.  
   - Tagged the image and pushed it to **Docker Hub** for centralized storage.  
   - This allows running the application consistently in any environment using Docker.

<img width="1879" height="410" alt="Screenshot 2025-10-27 142139" src="https://github.com/user-attachments/assets/127d6f98-590c-4ac8-a892-b53451fbe0e1" />

 **Deployment on Jenkins Server**  
   - Created a **Deploy job** in Jenkins to run the application.  
   - Pulled the Docker image from the **Docker Hub repository**.  
   - Allocated required **resources** for the container to ensure smooth execution.  
   - Exposed the application port so it can be accessed from outside the container.  
   - Verified that the container starts correctly after release.

**Application Access**  
   - Retrieved the **server IP** and the **exposed port**.
   - Accessed the application through a web browser to verify that it is running correctly.  
<img width="1078" height="352" alt="Screenshot 2025-10-27 155157" src="https://github.com/user-attachments/assets/2b4d6646-a8f6-409b-b551-44cb7b2420ab" />
   - Tested application functionality:
   - added items,
     <img width="1353" height="903" alt="Screenshot 2025-10-27 161513" src="https://github.com/user-attachments/assets/e92e7b71-61ee-486c-8549-aea24d39d7d1" />

   -  created a new user and ensured the app behaves as expected.
<img width="1405" height="458" alt="Screenshot 2025-10-27 161542" src="https://github.com/user-attachments/assets/2377c66f-ddae-4ddd-941e-8e7d4417d6f6" />
<img width="1112" height="58" alt="Screenshot 2025-10-27 161607" src="https://github.com/user-attachments/assets/0c40b222-5a10-48b2-b0e5-5f42a77ed7d3" />







