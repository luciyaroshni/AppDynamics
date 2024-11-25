
# AppDynamics — Installing and Configuring Machine Agent on a Windows Machine

This guide provides step-by-step instructions for installing and configuring the AppDynamics Machine Agent on a Windows machine. The Machine Agent is used to monitor server health and performance by collecting key hardware metrics like CPU, memory, disk, and network usage. It covers downloading the agent binary, configuring the controller-info.xml file, testing the agent, and installing it as a Windows service, enabling integration with the AppDynamics Controller for server monitoring.


There are two methods to download the Machine Agent binary files:

1. From the SaaS Controller: Download directly via the SaaS Controller interface.
2. From AppDynamics Account Portal: Access specific versions by visiting accounts.appdynamics.com/.

When downloading the Machine Agent from accounts.appdynamics.com instead of the SaaS Controller, the process is as follows:

Log in to your AppDynamics account.
Navigate to the Downloads section and select the desired agent type.
Choose the version and operating system for the Machine Agent.
Click Download to retrieve the binary file.

![image](https://github.com/user-attachments/assets/f944dfda-272c-4396-ba92-7c5feb3944f6)

![image](https://github.com/user-attachments/assets/71115bb5-1f51-45d6-93f4-07fe9f511752)

When downloading from this location, the controller-info.xml file will not include pre-configured controller settings, requiring manual configuration of properties such as controller host, port, and account details.

To download the Machine Agent from the SaaS Controller:

Log in to your SaaS Controller.
Navigate to the Server section and click on Get Started.

![image](https://github.com/user-attachments/assets/c6fc916f-c7d9-4ac6-8b59-1d5d9ced05ba)

Select the appropriate platform bundle for your operating system.

![image](https://github.com/user-attachments/assets/f223a9ab-5bd9-4a59-bd07-d7aac50705e6)

Scroll down and click Download the Agent to initiate the download.

![image](https://github.com/user-attachments/assets/d9982f39-b5a4-498b-8821-9bec6b84b966)

Copy the agent to your Windows machine and extract the zip file.

![image](https://github.com/user-attachments/assets/5962ce6e-e9bc-4b31-8aef-e63f4b75118a)

Before installing the Machine Agent, you need to configure a few essential properties:

Locate Configuration File: Navigate to the conf/ folder in the extracted agent files and open the controller-info.xml file.

This file contains key properties like the controller host, port, and connection settings required for the agent to communicate with the AppDynamics Controller.

If the agent file is downloaded from the SaaS Controller, the controller details will already be pre-configured.

![image](https://github.com/user-attachments/assets/6dd67376-ed5d-4d0b-bdfc-e688cfee5cd3)

![image](https://github.com/user-attachments/assets/443699c7-e1a9-4fae-80d8-e5dd45f8bef2)

To test the Machine Agent after configuration, open a command prompt and navigate to the directory where the agent files are extracted.

Run the following command to execute the agent

```
java -jar machineagent.jar
```

![image](https://github.com/user-attachments/assets/31740c75-b530-4781-8278-c91620b6683c)

![image](https://github.com/user-attachments/assets/6648f4d0-e96f-4139-bbed-77ed22ddd399)

It confirms that the Machine Agent is correctly configured and functioning. You can now proceed with installing the agent as a service on your machine.

To install the Machine Agent as a service, navigate to the location where you extracted the agent files. Right-click on the InstallService.vbs file and select Run as administrator to install the service.

![image](https://github.com/user-attachments/assets/073b1931-ba62-4414-acce-55d96f4029e2)

![image](https://github.com/user-attachments/assets/12ddc9fe-9df4-4645-86fa-54aeb22c26b5)

Once the service is installed, you can verify its installation.

![image](https://github.com/user-attachments/assets/f1941c43-c98a-4f32-8630-09fef4b6e337)

As you can see the agent is running successfully.

To verify if the Machine Agent is running as expected, you can also navigate to the logs/ folder within the agent’s installation directory.

Look for the log file named machineagent.log.

Open the log file and review the entries to ensure that the agent is functioning correctly and no errors are occurring.

![image](https://github.com/user-attachments/assets/599b4730-5846-44b4-b5f1-ba263ff9d71f)

After verifying that the Machine Agent is running correctly, return to the AppDynamics Controller. Click on Continue to proceed with the next steps in your setup or configuration.

I can see the server details are coming.

![image](https://github.com/user-attachments/assets/73220462-ded7-4391-ad73-b89200f8988d)

The server health is in critical condition and as I drill down, I realized it is showing the “Machine availability too low”

![image](https://github.com/user-attachments/assets/b0705f0c-1162-4674-b9b5-9cd6b787b018)

![image](https://github.com/user-attachments/assets/47fcaf26-9b2d-4208-9f87-911c5ecaab47)

If you’ve followed these steps, the Machine Agent should now be running and connected to your AppDynamics Controller, ready to monitor your system’s health and performance.




