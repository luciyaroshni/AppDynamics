
# AppDynamics — Installing Machine Agent on a Linux Server

Today, we will learn how to install the AppDynamics Machine Agent on a Linux server. The first step involves downloading the necessary binaries. Here’s how:

This time, we will download the binaries from account.appdynamics.com

Open a web browser and navigate to account.appdynamics.com.

Log in using your credentials.

Once logged in, go to the Downloads section.

![image](https://github.com/user-attachments/assets/427d11d8-94d4-4bba-8d21-164d6771932b)

In the Downloads section, select Machine Agent as the agent type.

Choose the Latest Version to ensure you’re using the most up-to-date features and fixes.

For the Operating System, select Linux.

Instead of directly clicking the Download button, locate the option to generate a cURL command.

![image](https://github.com/user-attachments/assets/dec3b7f5-a7cb-47ad-938d-4fde1c37619e)

![image](https://github.com/user-attachments/assets/15c498a7-4a5a-4e15-9d4c-3a862f2747c5)

Once you copied the curl command, login to your machine and run it.

![image](https://github.com/user-attachments/assets/f32838a4-1191-4440-a87f-786759f6a522)

![image](https://github.com/user-attachments/assets/f510fc2f-020c-4bb7-a606-7695c9730c90)

You will be able to see the machine agent on the location.

![image](https://github.com/user-attachments/assets/a9955662-1b73-4bc8-bb96-aa31e40413d1)

Extract the Machine Agent Files.

```
unzip <agent-file-name>.zip -d machine-agent
```

![image](https://github.com/user-attachments/assets/89deb9dd-a92d-4eed-af81-16904873a3cf)

Navigate to that machine-agent folder and you will be able to see the relevant files are extracted.

![image](https://github.com/user-attachments/assets/744df607-6501-48fb-beca-436f524b0ee5)

The first step in configuring the machine agent is to set the required properties in the controller-info.xml file. To do this, navigate to the conf folder and open the file.

```
cd conf
```

```
nano controller-info.xml
```

Since you downloaded it directly from the site, you will need to manually enter the details.

Provide the controller host and port 443.

![image](https://github.com/user-attachments/assets/65d66451-8e70-4e96-b1a0-d3b8396d3a39)

Enable SSL to be equal to True since we are using HTTPS to connect.

![image](https://github.com/user-attachments/assets/5b2523a0-863b-4889-b7f0-1eff003b188b)

Provide account access key and account name.

![image](https://github.com/user-attachments/assets/731d5518-d8fe-4b32-aaf8-97e23c79dfa7)

Enable sim-enabled to true for server monitoring.

![image](https://github.com/user-attachments/assets/4314bac3-5b5c-4950-9602-5f279cf85089)

Let’s proceed and test if it’s working correctly.

```
MACHINE_AGENT_HOME/jre/bin/java -jar MACHINE_AGENT_HOME/machineagent.jar
```

I can see the machine agent started successfully.

![image](https://github.com/user-attachments/assets/057821f3-e04c-4b1a-98c2-2ef14e11e4aa)

Verify it on the controller.

![image](https://github.com/user-attachments/assets/9a5f5129-637e-4bd7-ad12-6993c6a558a5)

Now stop the testing and proceed with the installation.

We need to create a directory under the /opt folder and place the binaries there so that the machine agent service can read the file from this location and run properly.

Navigate to /optfolder.

Make a directory called appdynamics and navigate inside that folder.

![image](https://github.com/user-attachments/assets/727f6d51-dc19-4ff2-ad72-37ed006aa89b)

Copy the binary file to inside the opt/appdynamics

![image](https://github.com/user-attachments/assets/00787d17-2692-43dd-a17b-527093bee7e7)

The next step is to copy the .service file to install the agent. Let's proceed by copying the .service file from the machine agent’s etc folder to the root etc folder.

Navigate to the etc folder inside the machine agent folder.

```
cd /opt/appdynamics/machine-agent/etc/systemd/system
```

![image](https://github.com/user-attachments/assets/8f41d264-232e-4112-950b-19e21d341c50)

I can see the machine-agent.service file in the specified folder. Let's copy it to the root's etc/ folder.

```
sudo cp appdynamics-machine-agent.service /etc/systemd/system
```

![image](https://github.com/user-attachments/assets/e2db3069-8aa0-4dcb-83a7-2f0755a439c2)

We will be running that copied file to install the agent. Before proceeding, we need to edit the file.

The first thing we need to verify is if the machine agent home directory is correct.

![image](https://github.com/user-attachments/assets/ee156917-f3c0-4e7a-80eb-280610f1c348)

Next, we need to update the username under which the service is running. In an enterprise scenario, a specific user with read-write permissions to the machine agent folder is typically created. However, since I don’t have a dedicated user for this, I will change it to ‘root’ in my case.

![image](https://github.com/user-attachments/assets/15d4afc1-4a1e-4b7f-85b6-e7fb1e8ef199)

To run this service, the first thing we need to ensure is that the necessary permissions are granted to the AppDynamics service and the /opt/appdynamics folder.

To install the agent, we will be using systemctl command.

Enable the service using systemctl command.

```
sudo systemctl enable appdynamics-machine-agent.service
```

![image](https://github.com/user-attachments/assets/92be6df7-0ee0-4097-bca5-117b9f21be0c)

Start the service.

```
sudo systemctl start appdynamics-machine-agent.service
```

Check whether the service is running:

```
sudo systemctl start appdynamics-machine-agent.service
```

![image](https://github.com/user-attachments/assets/27cf1cab-f99b-42c5-b632-979453b465ee)

I can see the agent is successfully reporting now.

![image](https://github.com/user-attachments/assets/7cd75238-2f38-4d29-a8db-8c7511120cd9)


<l><b>Troubleshooting:</b></l>

I ran into one of the following error.

```
<head>
    <meta charset="UTF-8">
    <title>Unauthorized</title>
</head>
<body>
HTTP Error 401 Unauthorized
<p/>
This request requires HTTP authentication
</body>
</html>
 at com.appdynamics.voltron.rest.client.VoltronErrorDecoder.decode(VoltronErrorDecoder.java:62) ~[rest-client-1.1.0.332.jar:?]
 at feign.SynchronousMethodHandler.executeAndDecode(SynchronousMethodHandler.java:156) ~[feign-core-10.7.4.jar:?]
 at feign.SynchronousMethodHandler.invoke(SynchronousMethodHandler.java:80) ~[feign-core-10.7.4.jar:?]
 at feign.ReflectiveFeign$FeignInvocationHandler.invoke(ReflectiveFeign.java:100) ~[feign-core-10.7.4.jar:?]
 at jdk.proxy2.$Proxy116.registerMachine(Unknown Source) ~[?:?]
 at com.appdynamics.agent.sim.registration.RegistrationTask.run(RegistrationTask.java:195) [machineagent.jar:Machine Agent v24.10.0.4455 GA compatible with 4.4.1.0 Build Date 2024-10-29 08:21:05]
 at java.util.concurrent.Executors$RunnableAdapter.call(Unknown Source) [?:?]
 at java.util.concurrent.FutureTask.runAndReset(Unknown Source) [?:?]
 at java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(Unknown Source) [?:?]
 at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) [?:?]
 at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) [?:?]
 at java.lang.Thread.run(Unknown Source) [?:?]
```

The issue was caused by an incorrect account name specified in the controller-info.xml file.









