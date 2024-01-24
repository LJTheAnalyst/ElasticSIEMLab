<h1>Elastic SIEM - Mastering Event Management</h1>

<h2>Description</h2>
This is a comprehensive guide detailing the process of creating an Elastic Stack Security Information and Event Management (SIEM) home lab using the Elastic Web portal and a Kali Linux virtual machine (VM) using Oracle VM Virtualbox. The core focus for this project is to further my experience with generating and analyzing security events, setting up agents for log forwarding, creating threat detection rules, establishing security alerts, and creating dashboards for analysis. Using the VM environment I will generate events using the Kali terminal then configure an agent to forward data to the SIEM, query and analyze the logs in the SIEM, then create a dashboard for visual data analysis and communication with key stakeholders.
<br/>
<br><img src="https://imgur.com/HDQrL5c.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>



<h2>Key Learnings</h2>

<br> From my Elastic SIEM home lab project, I extracted several key learnings that boosted my security analysis and threat detection skills:
- Understanding the security event lifecycle: I gained practical experience generating, collecting, analyzing, and responding to security events, simulating real-world attacks to see the full cycle in action.
- Log forwarding mastery: Utilizing agents like Elastic Defend, I learned how to efficiently collect logs from diverse sources and centralize them in Elastic SIEM for comprehensive analysis.
- Data visualization for insight: Crafting custom dashboards in Kibana transformed raw data into actionable insights, allowing me to visualize trends, identify vulnerabilities, and monitor security posture effectively.
- Proactive threat hunting: Creating and fine-tuning custom detection rules empowered me to actively hunt for threats in the logs, catching suspicious activity before it could escalate.
- Alerting without the exhaustion: By configuring different alert levels and notification channels, I learned to balance timely awareness of critical threats with avoiding being overwhelmed by trivial events. </br>

This project solidified my understanding of the core pillars of SIEM: log collection, analysis, visualization, detection, and alerting. It equipped me with valuable skills to apply in real-world security monitoring and threat defense scenarios.
<br/>


<h2>Utilities Used</h2>

- <b>Elastic SIEM</b>
- Kali Terminal
- <b>Log Files</b>


<h2>Environments Used </h2>

- <b>Oracle VM Virtualbox</b> 
- <b>Kali Linux</b>

<h2>Links</h2>

- <b>Elastic (ELK) SIEM:</b> https://cloud.elastic.co/registration
- <b>Kali VM Download:</b> https://www.kali.org/get-kali/#kali-platforms   
- <b>Oracle VM Virtualbox:</b> https://www.virtualbox.org/


<h2>Program walk-through:</h2>

<p align="center">

<h3><b>Step 1: Set up an Elastic Account</b></h3>
<br/>

The first thing I did was create a new Elastic Cloud account and create a new deployment. Elastic provides security teams with visibility, threat hunting, automated detection, and Security Operations Center (SOC) workflows. Severity and risk scores associated with signals generated by the detection rules enable analysts to rapidly triage issues and turn their attention to the highest-risk work. <br/>
<br><img src="https://imgur.com/IicxmsJ.png" height="80%" width="80%" alt="Nessus Essentials"/> <br/>
<br />


<h3><b>Step 2: Download Kali Linux and Install to VirtualBox</b></h3>
<br />

I downloaded the Kali Linux VM and installed it to Oracle VM VirtualBox. I then completed the Kali Linux installation and logged to verify a successful installation. <br/>
<br><img src="https://imgur.com/s4ob5fY.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/CdSZrut.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/v4EfRWw.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/G0OYFTv.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/Xfk8lnU.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/hGyOtUV.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/G0OYFTv.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/Xfk8lnU.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br/>


<h3><b>Step 3: Configure the Elastic Agent on the Linux VM to collect the logs and forward it to the SIEM</b></h3>
<br />

To forward the logs, I will be using Elastic Agent. Elastic Agent is a single, unified way to add monitoring for logs, metrics, and other types of data to a host. It can also protect hosts from security threats, query data from operating systems, forward data from remote services or hardware, and more. This is done by installing the Elastic integrations which provide an easy way to connect Elastic to external services and systems, and quickly get insights or take action. <br/>
<br>To Install the agent on my Kali VM I have to install the necessary integrations. I will select the “Elastic Defend” and follow the instructions to install the Elastic agent on my Kali VM in the Kali terminal. The Elastic Defend Integration will provide the VM with prevention, detection, and response capabilities with deep visibility for EPP, EDR, SIEM, and Security Analytics.</br>
<br><img src="https://imgur.com/uiyzSNn.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/TSoupcP.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/v74D5Ky.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Being that I am using Linux on my VM, I will make sure “Linux” is selected and then copy that command to my clipboard and paste that command into the Kali terminal. <br/>
<br><img src="https://imgur.com/v7hITu3.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/mBsvup6.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To verify that the agent successfully downloaded, I will use the terminal command ‘sudo systemctl status elastic-agent.service’. Additionally, inside of the Elastic interface I am able to see that a new endpoint was added, which is the host named ‘kali’. <br/>
<br><img src="https://imgur.com/TxGDcwT.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/r8d1Cs9.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/JKHTl9k.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/fNrOVIT.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br />


<h3><b>Step 4: Generating Security Events on the Kali VM using Nmap</b></h3>
<br/>

Next, I will run some Nmap scans on my Kali VM’s IP address to generate security events in Elastic. Nmap (Network Mapper) is an open-source utility used for network exploration, management, and security auditing. It is designed to discover hosts and services on a computer network, thus creating a “map” of the network. Nmap can be used to scan hosts for open ports, determine the operating system and software running on the target system, and gather other information about the network <br/>
<br>I ran a few Nmap scans to generate several security events, such as the detection of open ports and the identification of services running on those ports.</br>
<br><img src="https://imgur.com/4As1eNM.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br />


<h3><b>Step 5: Querying for Security Events in the Elastic SIEM</b></h3>
<br/>

Now that I have forwarded data from the Kali VM to the SIEM, I can start querying and analyzing the logs in the SIEM, and also search for specific security events using Elastic’s web interface. To search and access the logs, I navigated to the Logs page in Elastic under observability. <br/>
<br><img src="https://imgur.com/0yT1QLl.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>I then used the process.args: “nmap” command to display the Nmap events created on your Kali VM. This command is a part of Kibana Query Language (KQL) which is a simple text-based query language for filtering data inside of the SIEM. I was also able to view additional details about each event. The image below shows that the SIEM was able to detect the nmap scan of the endpoint IP address. <br/>
<br><img src="https://imgur.com/r1aHJcy.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/dNEBjkz.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br/>


<h3><b>Step 6: Create a Dashboard to Visualize the Events</b></h3>
<br/>

Below I will be creating a simple dashboard to visualize the count of security events over time.  <br/>
<br><img src="https://imgur.com/1grru0I.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/sxnQvmw.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>For the first visualization, I selected “Bar vertical stacked” as the chart type. This will create a chart that shows the count of events over time. <br/>
<br><img src="https://imgur.com/TRnxctj.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>In the “Metrics” section of the visualization editor on the right, select “Count” as the vertical field type and “Timestamp” for the horizontal field. This will show the count of events over time.<br/>
<br><img src="https://imgur.com/UyIjKbw.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>A title was added to the chart, the name of the horizontal and vertical axis was changed, and the visualization was saved to the dashboard.<br/>
<br><img src="https://imgur.com/c1C3vwE.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To add more visualizations to the dashboard, additional events will be created from the kali terminal.<br/>
<br><img src="https://imgur.com/oeFcbZs.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br/>

<h3><b>Step 7: Create an Alert </b></h3>
<br/>

I will be creating an alert in Elastic SIEM to detect Nmap scans based on custom queries. Alerts serve as a vital component in a SIEM system, ensuring prompt detection and response to security incidents. These alerts are crafted based on predefined rules or customized queries, tailored to trigger precise actions when specific conditions are met. <br/>
<br><img src="https://imgur.com/eBTxI9n.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>The first step is to create and define a new rule. <br/>
<br><img src="https://imgur.com/5T6CP5y.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/UZJU49h.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/3jyJaGN.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Under “Custom query,” I typed event.action: “nmap_scan” which is the condition for the rule and will match all events with the action “nmap_scan.<br/>
<br><img src="https://imgur.com/pOIuGDx.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Under the “About rule” section I set the default severity level to high with a Default risk score of 85.<br/>
<br><img src="https://imgur.com/SNevBnd.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Runtime for rules are adjusted under “Schedule rule”. Being that this alert was set to a severity level of high, I will schedule this alert to run every 5 minutes.<br/>
<br><img src="https://imgur.com/5Mdq3gR.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>In the “Actions” section, I will select the action of email to send when the rule is triggered which will be configured with SMTP. <br/>
<br><img src="https://imgur.com/9bn5v8Z.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/2nNRMfE.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/Yxomh5r.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Following a new nmap scan, it is displayed that the scan was detected and included in the dashboard.<br/>
<br><img src="https://imgur.com/7Sf5lT2.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Additional panels were added to the dashboard to display analytics for event logs. These visualizations are based on rules created from custom queries. Custom queries are query-based rule, which searches the defined indices and creates an alert when one or more documents match the rule’s query.<br/>
<br><img src="https://imgur.com/J8GyfO7.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br/>
</p>
