# AWS Medical Information AI Voice Conversion

## Implementation of Functionality for converting Medical Information into Natural Speech in Multiple Languages Using AWS Artificial Intelligence Services (Amazon Polly & Amazon Translate)

<p align="center">
<img src="https://i.imgur.com/xsfS2Tn.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Description
This project involves implementing a serverless solution on AWS to convert medical information into natural speech in multiple languages using Amazon Polly and Amazon Translate. The solution features secure authentication via Amazon Cognito, data hosting on Amazon S3, backend processing with API Gateway and AWS Lambda, and storage in DynamoDB. The architecture ensures scalability, security, and real-time processing and is ideal for multilingual healthcare applications.

<p align="center">
<img src="https://i.imgur.com/YD8C8aG.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

This project implements a serverless solution on AWS to convert medical information into natural speech in multiple languages using Amazon Polly and Amazon Translate.
 
## Project Objectives
1.	Automate the transcription of doctor-patient audio conversations into text.
2.	Ensure support for multiple languages, including English and Portuguese.
3.	Provide secure storage of transcriptions in medical records for easy retrieval.
4.	Leverage a hybrid cloud approach using Azure AI Speech Service for transcription and AWS for backend infrastructure.
5.	Implement real-time monitoring and logging to ensure system reliability.
6.	Optimize resources to minimize costs and ensure scalability for future enhancements.

## Project Solution
### Part 1: Azure AI Speech Service and Backend Setup
1.	Azure Speech Service Configuration:
    - Set up Azure Speech Service and retrieved the speech key and region.
    - Tested transcription in English and Portuguese for accurate recognition.
2.	Deploy HealthHub Backend:
    - Downloaded and unzipped application files.
    - Installed necessary dependencies.
    - Configured Azure credentials for transcription and deployed backend services to process audio files.

### Part 2: Frontend Deployment and Transcription Testing
1.	Deploy HealthHub Frontend:
    - Configured the API base URL to connect with the backend.
    - Deployed the frontend application for user interactions.
2.	System Testing:
    - Registered a doctor and patient.
    - Uploaded and processed audio conversations in both English and Portuguese.
    - Verified transcription accuracy and saved the text into the patient's medical records.
3.	Explored Azure Speech Service Metrics:
    - Monitored service usage and analyzed transcription performance metrics, including latency and service availability.

## Tools and Technologies
1.	Azure AI Speech Service: For multilingual audio-to-text transcription.
2.	AWS Components:
    - Amazon Cognito: For user authentication and authorization.
    - Amazon S3: To store application-related files.
    - AWS API Gateway: For managing API requests.
    - AWS Lambda: For serverless backend execution.
    - Amazon DynamoDB: To store transcribed text in patient medical records.
    - Amazon CloudWatch: For monitoring and logging.
    - AWS CloudFormation: For provisioning and managing resources.
3.	HealthHub Application: Frontend and backend systems for interaction with transcription services.
4.	Languages and Frameworks: Python for backend development and RESTful APIs.

## Step-by-Step Directions
### Part 1: Backend Implementation
#### Step 1: Preparing the Environment
1. Launching the EC2 Workstation
    - Start the EC2 instance used for development.
 <p align="center">
<img src="https://i.imgur.com/6OnGHHy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/LGDqoMV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Downloading and Unzipping Project Files
    - Use the command:
<p align="center">
<img src="https://i.imgur.com/Sg1U67f.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
    - Navigate to the backend folder:
<p align="center">
<img src="https://i.imgur.com/JcBXKQG.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
    - Check backend files
 <p align="center">
<img src="https://i.imgur.com/3vg1qdk.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/BrPex8z.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Installing Backend Dependencies
    - Install the required Node.js dependencies for the backend and its services:
 <p align="center">
<img src="https://i.imgur.com/jTx6N7Y.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/U0LLnpC.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Step 2: Deploying HealthHub Backend Services
1. Deploy All Services
<p align="center">
<img src="https://i.imgur.com/eLkmYCb.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
    - Monitor the deployment process through CloudFormation stacks to ensure all resources are created without errors.
 <p align="center">
<img src="https://i.imgur.com/HGRZHDI.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/KFUhAZF.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/rshBrRL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/3GvdgK0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
    - Check for application creation errors
<p align="center">
<img src="https://i.imgur.com/BJAfmrZ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Deploy Individual Services (Optional)
    - Example for the AI Interaction Service:
    - `serverless deploy --stage dev --service ai-interaction-service`

#### Step 3: Validating the Deployment
1. Check CloudFormation Stacks
    - Validate that all resources, including Lambda functions, DynamoDB tables, and API Gateway endpoints, have been created.

2. Verify Lambda Functions
    - Confirm the presence of the function:
    - `hh-ai-interaction-dev-getInteraction`

#### Step 4: Reviewing the Code
1. Serverless Configuration
    - Review serverless.yml to understand the services, provider configurations, and resource definitions.
<p align="center">
<img src="https://i.imgur.com/0Q0gABy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. AI Interaction Service
    - Explore aiInteractionService.ts to understand how Amazon Polly is used for voice synthesis and Amazon Translate for text translation.
<p align="center">
<img src="https://i.imgur.com/iZbaL8H.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. DynamoDB Table
    - Verify actions like InsertItem and WriteItem configured for storing interactions.
<p align="center">
<img src="https://i.imgur.com/Q3YuYVs.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Part 2: Frontend Implementation
#### Step 5: Setting Up the Frontend
1. Navigate to Frontend Folder
    - Move to the frontend directory:
<p align="center">
<img src="https://i.imgur.com/g0aZaaZ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Install Dependencies
    - Run:
<p align="center">
<img src="https://i.imgur.com/mzvH13n.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Step 6: Configuring the API Base URL
1. Set the API Gateway Endpoint
    - Copy .env.example to .env and edit the base URL:
    - Use the API Gateway endpoint URL from the deployment process.
<p align="center">
<img src="https://i.imgur.com/gCqtjUR.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/vaI39WZ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Update Tailwind Configuration (if needed):
    - Rename the configuration file:
<p align="center">
<img src="https://i.imgur.com/Tv7I3jG.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/6UIUct4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Step 7: Running the Frontend Application
1. Start the Application
    - Run the application:
<p align="center">
<img src="https://i.imgur.com/2lGX2ds.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Access the Application
    - Open the application using the EC2 instance's public IP address and port 5173:
<p align="center">
<img src="https://i.imgur.com/ndu4qaQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/5N3Zf2v.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Step 8: Adding Users
1. Register a Doctor
    - Example:
        - Email: david.lee@hh.com
        - Password: 123456
        - Role: Doctor
        - Other Details: Radiology, License Number 111111
<p align="center">
<img src="https://i.imgur.com/RWzoWtL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
2. Register a Patient
    - Example:
        - Email: ava.brown@tcb.com
        - Password: 123456
        - Role: Patient
<p align="center">
<img src="https://i.imgur.com/2uakWTg.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
#### Step 9: Testing the AI Speech Feature
1. Log in as a Doctor
    - Use the credentials created in the previous step.
 <p align="center">
<img src="https://i.imgur.com/4LLDnbJ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Generate AI Speech
    - Test with sample medical instructions in multiple languages, such as English and Portuguese.
<p align="center">
<img src="https://i.imgur.com/WbHBAZz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
3. Validate Speech Conversion
    - Ensure the speech is saved in the patient's medical records.

4. Monitor Metrics
    - Use Amazon Translate and CloudWatch to check API calls and logs.
<p align="center">
<img src="https://i.imgur.com/UFoDXaL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/E5c9bCX.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/mwVIjgv.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
<p align="center">
<img src="https://i.imgur.com/cYazlQH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/NGeZoVw.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />
 
## Conclusion
The project successfully delivered an end-to-end system for transcribing doctor-patient conversations into text. The integration of Azure AI Speech Service with AWS components enabled seamless transcription and storage in a secure and scalable manner. Multilingual support ensured the system's adaptability for diverse user needs.

### Challenges Encountered
1.	Multilingual Transcription Accuracy: Initial misrecognition of certain accents required fine-tuning of Azure Speech Service configurations.
2.	API Integration: Ensuring smooth communication between frontend and backend systems presented some debugging challenges.
3.	Cost Management: While testing, controlling resource usage required active monitoring to minimize expenses.

### Lessons Learned
1.	Proper configuration and testing of Azure AI Speech Service are critical for achieving high transcription accuracy.
2.	Real-time monitoring using CloudWatch is invaluable for detecting and addressing system performance issues promptly.
3.	Hybrid cloud architectures (Azure + AWS) can enhance functionality but require careful orchestration and compatibility testing.

### Future Improvements
1.	Enhanced Language Support: Expand the system to support additional languages to cater to a broader audience.
2.	Real-Time Transcription: Implement streaming transcription for live consultations.
3.	User Interface Enhancements: Improve the frontend interface for easier interaction and better usability.
4.	Cost Optimization: Explore AWS Savings Plans and Reserved Instances for predictable workloads to reduce operational costs further.
