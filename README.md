# HealthHub: Deployment of A 100% Serverless Application on AWS Using Amazon Congnito, S3, API Gateway, Dynamodb, and Amazon Lambda Services Via Cloudformation

<p align="center">
<img src="https://i.imgur.com/HjkyCIb.png" height="80%" width="80%" alt="HealthHub Architecture"/>
<br />
<br />

## Project Description
The Health Hub project is a cloud-based healthcare application designed to facilitate interactions between patients and doctors. It employs a serverless architecture using AWS to ensure scalability, flexibility, and cost-effectiveness. The application's features include user registration, secure management of appointments, and easy retrieval of medical records. In addition, this foundational structure sets the stage for integrating artificial intelligence capabilities such as text-to-speech and language translation. Through a phased approach, the project focuses on building, testing, and refining the architecture while ensuring resource optimization and cost management.

## Project Objectives
1. **Establish Serverless Architecture**: Build and deploy a serverless backend leveraging AWS services for scalability and performance.
2. **Ensure Secure Data Handling**: Implement security measures for managing sensitive healthcare data while maintaining accessibility.
3. **Develop Modular Functionality**: Design reusable components in the application to support the addition of advanced features over time.
4. **Optimize Deployment Processes**: Create efficient workflows for deploying, testing, and cleaning up resources after each phase.
5. **Lay the Groundwork for AI Integration**: Prepare the system for the integration of AI services such as Amazon Polly and Amazon Translate in subsequent stages.

## Project Solution
### Part 1: Backend and API Configuration
- Set up a secure backend using AWS Lambda, API Gateway, and DynamoDB.
- Configure endpoints to enable seamless API communication for user management, appointments, and data retrieval.
- Verify functionality through API testing and log inspection.

### Part 2: Frontend Development and Integration
- Install and configure the frontend using Vite.
- Set up package dependencies using npm and link the frontend to the backend API through environment variables.
- Deploy static files to Amazon S3 for hosting.

### Part 3: Application Testing and Resource Cleanup
- Deploy and test the integrated frontend and backend system by registering users, scheduling appointments, and verifying data flow.
- Handle security configurations, including enabling ports and editing inbound rules in AWS Security Groups.
- Demonstrate resource cleanup using the SLS remove command and manually deleting AWS services left undeleted by CloudFormation.

## Tools and Technologies
### 1. Cloud Services:
- AWS Lambda
- Amazon API Gateway
- Amazon DynamoDB
- Amazon S3 (static site hosting)
- Amazon CloudFormation
- Amazon EC2 (workstation)

### 2. Programming and Development Tools:
- Node.js (Backend development)
- Vite (Frontend development)
- npm (Package management)

### 3. Version Control and Testing Tools:
- GitHub (Repository management)
- Postman (API testing)
- VS Code (Integrated development environment)

## AWS Cloud Architecture Project Solution (Parts 1, 2, and 3)
### Step-by-Step Instructions
#### Part 1: Setting Up the Base Architecture
##### Step 1: Setting Up the AWS Environment
1. **Login to AWS Console**:
   - Navigate to the AWS Management Console.
   - Ensure you are using the correct AWS region (e.g., us-east-1).

2. **Create an IAM Role**:
   - Navigate to IAM → Roles → Create Role.
<p align="center">
<img src="https://i.imgur.com/TW27eOx.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/KOyGz8b.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Choose AWS Service → EC2 → Next.
<p align="center">
<img src="https://i.imgur.com/V0YnbqW.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Attach the AdministratorAccess policy to allow full access.
<p align="center">
<img src="https://i.imgur.com/RkxhgEO.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Click Next → Review the details → Name the role tcb-hh-role.
<p align="center">
<img src="https://i.imgur.com/osUtMu7.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Complete the role creation process and take note of the role name.
<p align="center">
<img src="https://i.imgur.com/E9Uw8lz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
3. **Launch an EC2 Instance**:
   - Navigate to EC2 → Instances → Launch Instance.

##### Step 2: Launching the EC2 Workstation Instance
1. Launch an EC2 instance named tcb-hh-ws with the following configurations:
<p align="center">
<img src="https://i.imgur.com/rMIPiT4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Provide EC2 Instance with unique name (tcb-hh-ws)
<p align="center">
<img src="https://i.imgur.com/x6HNhu9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Select the Amazon Linux 2 AMI.
<p align="center">
<img src="https://i.imgur.com/fpX5jVL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Choose the t2.medium instance type 
   *Note: This instance type is not part of the AWS Free Tier!*
<p align="center">
<img src="https://i.imgur.com/XA3V5Bp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Create Key Pair
   - SSH Key: `tcb-hh-key`
<p align="center">
<img src="https://i.imgur.com/Azj60l9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - download the key pair file (.pem), and save it securely

   Under Security Groups, allow:
   - SSH (port 22) for your IP address.
   - HTTP (port 80) for public access
   - SG: `Allow SSH Traffic`
<p align="center">
<img src="https://i.imgur.com/PGet86x.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Storage: `30 Gib` | `gp3`
<p align="center">
<img src="https://i.imgur.com/sMfibD7.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Advanced details
   - IAM instance profile: `tcb-hh-role`
<p align="center">
<img src="https://i.imgur.com/ZZutPWx.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Click Launch Instance to Complete EC2 creation process 
<p align="center">
<img src="https://i.imgur.com/6eBxIqu.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Once launched, connect to the instance using the AWS Console SSH connection.
   Connect to the EC2 Instance:
   - Using the downloaded key pair, connect to the EC2 instance:
<p align="center">
<img src="https://i.imgur.com/TP65YTL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

##### Step 3: Preparing the Workstation
1. Validate the installation of AWS CLI, Node.js, NPM, and the Serverless Framework.
   Checking tools and services available
   - aws --version
   - node -v
   - npm -v
   - serverless --version
   - sls --version
<p align="center">
<img src="https://i.imgur.com/e8oXTQD.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Install Serverless Framework and Dependencies:
   - Download and run the NVM installation script from GitHub using curl and bash
<p align="center">
<img src="https://i.imgur.com/fXpbAgM.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Reload the shell configuration file to apply changes made by the NVM installer
<p align="center">
<img src="https://i.imgur.com/cxhFWMf.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Use NVM to download and install the latest Long-Term Support version of Node.js
<p align="center">
<img src="https://i.imgur.com/iLeDo2A.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Run a Node.js command that prints the message along with the current Node.js version
<p align="center">
<img src="https://i.imgur.com/tqafykB.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/S2IszZ0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
3. Install Serverless Framework version 3 globally using npm 
<p align="center">
<img src="https://i.imgur.com/knOvebF.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Display the installed version of the Serverless Framework using the 'serverless' command serverless --version
<p align="center">
<img src="https://i.imgur.com/knOvebF.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/NrKsB2Y.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Part 2: Implementing the Backend
##### Step 1: Setting Up Backend Files
1. HealthHub Backend Implementation
   - Installing Backend Project Dependencies
<p align="center">
<img src="https://i.imgur.com/FfFKMmV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/ZAV4oTP.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Navigate to the backend folder:
<p align="center">
<img src="https://i.imgur.com/PEn6mNp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
3. Review important files such as package.json and serverless-compose.yml for dependencies and configurations.
<p align="center">
<img src="https://i.imgur.com/n3FinkJ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/SLi4hvP.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   Inspect the Project Structure
   - Verify the project directory structure using the tree command
<p align="center">
<img src="https://i.imgur.com/WdkmO4i.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - The output should confirm proper setup.
<p align="center">
<img src="https://i.imgur.com/y1mtghr.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
##### Step 2: Installing Dependencies
1. Install dependencies for all service
<p align="center">
<img src="https://i.imgur.com/v2ZkQSv.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
##### Step 3: Deploy HealthHub Backend
The deployment of the backend requires setting up the necessary AWS services. Before deploying, confirm these AWS services are correctly configured:
- AWS Cognito
- IAM Roles
- AWS API Gateway
- AWS DynamoDB
- AWS S3 Bucket
- AWS CloudWatch Logs
- AWS Lambda

Run the deployment using the following command:
<p align="center">
<img src="https://i.imgur.com/lKgdgjA.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
- Verbose logs are available in ".serverless/compose.log"
<p align="center">
<img src="https://i.imgur.com/FynhxHo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
- Check for Errors 
<p align="center">
<img src="https://i.imgur.com/mLWOmF4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Validate the creation of AWS resources:
   - Open CloudFormation check stack processing....
<p align="center">
<img src="https://i.imgur.com/x3bzxnj.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/SRvlqPp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Check CloudWatch for Errors
<p align="center">
<img src="https://i.imgur.com/ccPdRbC.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/KkSi0t9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Check IAM Roles for created Roles
<p align="center">
<img src="https://i.imgur.com/Oj2NL4V.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/LDYVB8e.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Check API Gateway
<p align="center">
<img src="https://i.imgur.com/53Cscxa.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/ZGjWlkJ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/a0itrrc.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Check Amazon S3 for Buckets 
<p align="center">
<img src="https://i.imgur.com/HZ6MJTe.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/Yqj7cpD.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Check Lambda Functions
<p align="center">
<img src="https://i.imgur.com/at2EX6H.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/RvU3Guc.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Part 3: Frontend Implementation
After deploying the backend, proceed with the frontend implementation. This step involves installing dependencies and configuring the project environment for the frontend.

Installing Frontend Dependencies
- Navigate to the health-hub-frontend directory and install all dependencies:
<p align="center">
<img src="https://i.imgur.com/9mgt0z9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
- Check Frontend files in src directory
<p align="center">
<img src="https://i.imgur.com/1vVUW2o.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/we9o8v5.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/InMooQ9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
##### Step 2: Configuring the API Gateway URL
1. Copy and modify the .env file:
<p align="center">
<img src="https://i.imgur.com/EqX6azc.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/a7QdxSF.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
- Copy API Gateway URL
<p align="center">
<img src="https://i.imgur.com/kJMUQJk.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/I4u7hC9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Update the Vite API base URL with the API Gateway endpoint.
<p align="center">
<img src="https://i.imgur.com/Gz3kMmN.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
**Vite** is a frontend project build tool designed to offer a faster and lighter development experience for modern web projects.
1. Automatic exposure: These variables are automatically made available in the client code.
2. Main uses:
    - API URL Configuration: Allows defining the base API URL that the application will use.
    - Environment adaptation: Facilitates configuration changes between development, testing, and production.
3. Flexibility: Enables the use of different URLs (e.g., [http://localhost:3000] for development, [https://your-actual-api-url.com]for production) without changing the source code.
4. Advantages:
    - Cleaner code
    - Easy configuration changes between environments
    - Centralization of important settings

This method simplifies configuration management across different stages of application development.

##### Step 3: Running the Frontend
1. Run the application:
<p align="center">
<img src="https://i.imgur.com/koaT2kl.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/cyN0WcR.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Ensure the EC2 security group allows access to the application port (5173).
<p align="center">
<img src="https://i.imgur.com/gHzewjR.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
##### Step 4: Testing the Application
1. Access the application via the public IP address of the EC2 instance.
<p align="center">
<img src="https://i.imgur.com/Q03XwHH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/8KZjPeV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Add a doctor and a patient:
   - Doctor:
     - Email: david.lee@hh.com
     - Password: 123456
     - Specialization: Radiology
<p align="center">
<img src="https://i.imgur.com/qMOKDMi.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
   - Patient:
     - Email: ava.brown@tcb.com
     - Password: 123456
<p align="center">
<img src="https://i.imgur.com/kXUvDOK.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
3. Schedule an appointment as a patient and validate it as a doctor.
<p align="center">
<img src="https://i.imgur.com/pnXqzzB.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/MGsxwFx.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

With the completion of the foundational architecture and integration testing, the project is prepared for advanced modules involving AI services such as Amazon Polly and Amazon Translate. This systematic approach ensures that resources are efficiently used and lays the groundwork for implementing innovative features in subsequent modules.

## Project Conclusion
The Health Hub project successfully implemented a serverless cloud architecture for a scalable and secure healthcare application. The system's functionality was tested thoroughly in all aspects, including API communication, frontend-backend integration, and user interface workflows. The project also introduced a robust approach to managing and optimizing cloud resources, ensuring no unnecessary costs. While the project is complete for this phase, it paves the way for introducing AI technologies, which will enhance the application's capabilities further.

### Challenges Encountered
1. **Configuration Issues**: Initial configuration of API Gateway and environment variables required several iterations to resolve errors.
2. **Frontend Integration Bugs**: Issues such as Tailwind JS file extension conflicts required manual debugging and resolution.
3. **Resource Management**: Automating resource cleanup for AWS services involved troubleshooting residual components that were not removed by CloudFormation.

### Lessons Learned
1. **Importance of Proper Planning**: Setting up a robust architectural foundation requires thorough planning and iterative testing.
2. **Configuration Flexibility**: Using environment variables ensures seamless integration between backend APIs and frontend systems.
3. **Efficient Resource Cleanup**: Establishing consistent cleanup practices reduces unexpected costs and ensures efficient resource utilization.

### Future Scope
- **AI Integration**: Incorporate AI technologies, such as Amazon Polly for text-to-speech and Amazon Translate for multilingual support.
- **Enhanced User Features**: Add modules for more comprehensive healthcare services, such as medical history tracking and telemedicine.
- **Strengthening Security**: Implement HTTPS, multi-factor authentication, and encryption to further secure sensitive data.
- **Continuous Monitoring**: Integrate monitoring tools like AWS CloudWatch to improve observability and track application performance.
