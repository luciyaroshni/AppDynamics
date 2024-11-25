
# AppDynamics — NodeJs Installation

This documentation outlines the steps to integrate a Node.js application with AppDynamics for performance monitoring. The process includes how to install and configure the AppDynamics Node.js agent, link it to the SaaS controller, and verify the integration. Additionally, it covers generating application load, monitoring business transactions, analyzing transaction snapshots, and configuring a server agent for complete application and infrastructure visibility.

First, create an AppDynamics SaaS account by visiting their official website.

Click on Start a Free Trial.

![image](https://github.com/user-attachments/assets/fd57c276-2e3c-4d9e-859d-dddcee9abb27)

Fill in the required information.

![image](https://github.com/user-attachments/assets/91e85e10-45c2-45f9-bad2-1e8728a8b6da)

You will receive an email with your account details. After setting up your password, log in to your account by clicking the Launch button and entering your username and password.

Click on your profile, and from the dropdown, select Controller Tenants.

![image](https://github.com/user-attachments/assets/37af3584-a11d-43cb-a04c-6e05da3fec10)

This will open a new window as shown below.

![image](https://github.com/user-attachments/assets/f6f6bc1d-bc7a-4075-a622-699706bbd97d)

I will install the Node.js application agent and link it to this controller. Before proceeding, a Node.js application is required to integrate with AppDynamics. To host this application, I will create an EC2 instance in my AWS account and install the application to monitor using AppDynamics.

A Windows machine has been created for this purpose.

![image](https://github.com/user-attachments/assets/c115135c-0a6f-42f9-9559-ae82f3c0eb78)

To set up a Node.js application, search for ‘Node Express Cart’. Look for a link titled ‘express-cart — npm’.

Once you download it, you will receive a zip file. Extract the contents of the zip file.

![image](https://github.com/user-attachments/assets/c8caacd2-281a-43f0-8c63-0d4a26eacb8c)

To run this application, you need to install some dependencies. First, ensure that Node.js is installed on your system. Next, you will need to set up a MongoDB server. After that, follow the installation steps provided in the document.

I have configured my application.

![image](https://github.com/user-attachments/assets/03668795-6c77-40c1-9ee7-06cf47a40d38)

The next step is to install the Node.js agent.

To install the AppDynamics agent, go to the controller and click on the “Getting Started” section. Then, click on the “Getting Started Wizard.”

![image](https://github.com/user-attachments/assets/1521caac-ea21-4775-b559-98bbff180419)

Next, select the agent you want to install.

![image](https://github.com/user-attachments/assets/6b1dbc2d-e1f8-4f41-ad21-1cc76c7f5f0a)

Review the prerequisites, verify that the controller URL is correct, and then scroll down to the “Set Application and Tier” section.

![image](https://github.com/user-attachments/assets/a5aa78c1-e851-4c60-b748-017351065b24)

Enter an application name and a tier name.

![image](https://github.com/user-attachments/assets/f7ed2e9a-a823-48c7-b64f-427c8d6b9001)

Click on “Continue.”

After that, scroll down to find the instructions for installing the agent.

![image](https://github.com/user-attachments/assets/b8be53b1-8d06-4ce6-aa66-a13cfbd95fe0)

Run the npm install appdynamics command to ensure that the required dependencies are installed.

Don’t need to provide the version name unless have a specific requirement.

![image](https://github.com/user-attachments/assets/79797913-cd6a-459b-92ad-8307648998fb)

![image](https://github.com/user-attachments/assets/27990108-e23e-45a3-ab10-604c0a70aa94)

The AppDynamics dependencies have now been installed.

Next, you need to copy and paste the provided code into your application’s startup script.

If you’re working with another Node.js application and aren’t sure which file is the startup script, ask the application’s admin or support team for the correct file. This will ensure the code is placed in the right location.

![image](https://github.com/user-attachments/assets/08b4ceda-a89e-4a8e-aa17-b2abc9a1ea56)

The copied code should be pasted as the first line of the startup script, before any other dependencies are declared.

![image](https://github.com/user-attachments/assets/66cccecc-d81a-45f5-a6df-0f6e7d43dca6)

Verify the controller, account details, and application details. Once you’ve pasted the code, you can proceed to run the startup script to start the application and check if it is reporting to the controller.

To run the application, type node app.js.

![image](https://github.com/user-attachments/assets/6550c34d-5d5f-42bf-a629-ea3c4253f89e)

Once the application starts, return to the controller and check if the application is reporting.

Scroll down to the section where you can connect the agent to the AppDynamics controller.

![image](https://github.com/user-attachments/assets/9bbc5f2d-a35a-4da4-a02c-ae81614b8973)

Generate some load in the application to allow AppDynamics to capture the transactions.

Next, navigate to the Application section in the controller to verify the captured data.

![image](https://github.com/user-attachments/assets/2b80d49e-7c8e-4635-89be-9007fbc970b8)

You will see that the new nodejs_app has been created, and the metrics have already been captured.

Open the application to view the details and performance metrics.

![image](https://github.com/user-attachments/assets/c8d97b9c-0477-41f0-bc69-bded90018a4e)

You will see the generated call graphs. An “X” mark will appear in the MongoDB section since the agent hasn’t been installed there, but the application status will be green, indicating it is reporting. You can now view load, response times, errors, and other performance details.

Next, check the Business Transaction health to see the detailed performance of the transactions.

![image](https://github.com/user-attachments/assets/d3a63712-0bba-4418-91b3-2825237dc61f)

The transactions are now captured and displayed here. You can review their performance and any issues that may have occurred during processing.

![image](https://github.com/user-attachments/assets/a210e357-cacd-4b43-8c0e-482dd1e285d6)

Click on any of the transactions, and you will be able to view the captured call graphs, which provide a detailed flow of the transaction and highlight any performance issues or bottlenecks.

![image](https://github.com/user-attachments/assets/f7d3332e-cdea-47ec-8579-201b32867847)

Below is an example of a slow response time for one of the business transactions, indicating where delays might be occurring in the application flow.

![image](https://github.com/user-attachments/assets/67c6c1ab-5de6-4c02-b58d-6b82abc602a7)

It also provides a transaction snapshot, which allows you to view a detailed record of a single transaction as it moves through your application. This snapshot captures a series of events and performance metrics, offering insights into how the transaction was processed, identifying any bottlenecks or performance issues, and showing how long each component took to respond.

Double-click on the transaction snapshot to view more details.

![image](https://github.com/user-attachments/assets/00308b37-1621-4733-a704-3556d7052311)

You will then see an overview of the transaction.

![image](https://github.com/user-attachments/assets/3e4f9457-6333-41d8-b93d-8666b67f82b5)

If you click on the servers section, you will be able to see the server details. But as of now, we have not configured any agents to get the server information. So let’s do that as well.

Click on get started.

![image](https://github.com/user-attachments/assets/38a7b383-ba17-4342-b058-4ed64e150f96)

Choose the operating system and ensure that the controller URL is correct.

![image](https://github.com/user-attachments/assets/e71a23d9-6802-43c5-b56f-1288c9bd6b3e)

Scroll down, and you will find the section to download the agent.

![image](https://github.com/user-attachments/assets/6ef6ff6a-eaf4-433a-b44c-4e4e613592c0)

I have downloaded and extracted the agent on the server. Now, let me start the agent.

![image](https://github.com/user-attachments/assets/9b947ac7-c6f9-46a4-8c27-f0f5d161d174)

Run the provided command.

![image](https://github.com/user-attachments/assets/fd9da5c1-7645-4283-92f1-56023e66b72d)

On the controller, click on continue. You should then be able to see the server details appearing.

![image](https://github.com/user-attachments/assets/8ee94f3d-4fc2-4fb3-bfc6-31b0c6fdfb73)

![image](https://github.com/user-attachments/assets/c0b4416b-453c-4f54-92fc-94a488ef7f48)




