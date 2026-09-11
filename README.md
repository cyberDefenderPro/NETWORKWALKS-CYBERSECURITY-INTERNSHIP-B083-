<h2> NETWORKWALKS-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP</h2>


<h1>Project Overview</h1>
The Cybersecurity Lab Environment Setup project provides a fully virtualized, sandboxed network infrastructure designed for testing offensive security methodologies, 
defensive monitoring, and vulnerability analysis. By isolating virtual systems within a host-only network, the setup allows safe execution of attacks, threat analysis,
and security controls testing without risk to production environments or host systems.

<h3>Objectives</h3>


The main objectives of this project are to:

Install and configure VirtualBox.

Create a private NAT Network for the cybersecurity lab.

Install/import Kali Linux as a virtual machine.

Configure network connectivity for Kali Linux.

Assign a consistent IP address to the Kali VM.

Verify network connectivity and DNS resolution.

Take a clean VM snapshot for recovery.

Document the complete setup process.

Prepare the environment for future cybersecurity projects.


<h3>Purpose of the Lab</h3>

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

Network reconnaissance

Port scanning

Vulnerability assessment

Packet analysis

Web security testing

Exploitation practice

Security-tool experimentation


<h2>Lab Environment Installation and Configuration</h2>

<h3>Install and configure VirtualBox</h3>

Download and install Oracle VirtualBox.

<img width="597" height="352" alt="image" src="https://github.com/user-attachments/assets/e7c38ef0-e85e-4d07-963c-adad5749fe46" />


<h3>Create a private NAT Network</h3>
Create a private NAT network to allow the cybersecurity lab machines to communicate safely while maintaining internet access.
<h4>Steps:</h4>

Go to File>>Tools>>Networks>>NatNetworks>>Set IPv4 Prefix settings to 10.0.0.0/24>>Apply

<img width="347" height="523" alt="image" src="https://github.com/user-attachments/assets/c140d98c-ff52-4fee-a131-70a653fd742c" />


<h3>Install/import Kali Linux as a virtual machine</h3>

Download latest version of kali from its website. Extract file using WINRAR software.Import Kali Linux into VirtualBox and prepare it for use as the main cybersecurity testing machine.

<h4>Steps</h4>

Go to Virtual Box manu>> Machines>>Add>>Select Machine >>Open

<img width="394" height="304" alt="image" src="https://github.com/user-attachments/assets/c9a8d918-c518-4709-9ce4-19bf9b94eed0" />

<h3>Configure network connectivity for Kali Linux</h3>

Configure the Kali VM's network adapter so it can communicate with the lab network and access the internet when required.

<h4>Steps:</h4>

Go to Settings>>Network>>Select NatNetwork Previously created>>Ok

<img width="733" height="188" alt="image" src="https://github.com/user-attachments/assets/72be7005-73d5-4a44-b0a7-a79c0ff35fc4" />


<h3>Assign a consistent IP address to the Kali VM</h3>

Start Kali Virtual Machine.Configure IPV4 address manually to make network access and future lab activities easier.

<img width="468" height="384" alt="image" src="https://github.com/user-attachments/assets/329034ec-e09e-410c-a8a7-68310fa2db16" />


<h3>Verify network connectivity and DNS resolution</h3>

Test the network connection by browsing to confirm that internet service is working on Kali Linux .

<h3>Take a clean VM snapshot for recovery</h3>

Create a snapshot of the properly configured Kali VM so the lab can quickly be restored to a clean working state when required.
<h4>Steps:</h4> Shutdown Kali>>Go to snapshots>>Take Snapshot>>Set Name & Description>>ok

<img width="463" height="508" alt="image" src="https://github.com/user-attachments/assets/c91390c7-b0d9-4b47-93ee-847e2899d86e" />



<h3>Document the complete setup process</h3>

Record each configuration and setup step clearly so the environment can be recreated or reviewed later.

<h4>Lab is ready to support future cybersecurity exercises, testing, and learning activities.Additional Virtual machines like Windowd,Android can be added by following the same steps as required in the future</h4>
