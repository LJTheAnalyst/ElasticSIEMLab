<h1>Splunk Cloud in VirtualBox - Mastering Searches, Commands, Reports, and Dashboards</h1>

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

<h3><b>Part 1: VirtualBox Configuration and Data Upload</b></h3>
<br/>

Oracle VM VirtualBox is the Virtual Machine (VM) that I will download, configure, and manage this lab. I also downloaded the VirtualBox Extension Pack to support the VM. <br/>
<br><img src="https://imgur.com/OeSOJfK.png" height="80%" width="80%" alt="Nessus Essentials"/> <br/>
<br />
The first step of this lab is uploading the data that I will be querying and analyzing. I was able to access the the 'add data' feature from my Splunk cloud home page. The files that will be uploading includes access.log files, secure.log files, and vendor_sales.log files from mail servers and web accounts. Once the files were uploaded, I performed a basic search to ensure a successful upload.  <br/>
<br><img src="https://imgur.com/9FyAwXS.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/GUUa05K.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/ZgUNOdq.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/csXbN2D.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/KLZgxHm.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/G7EM1dv.png" height="80%" width="80%" alt="Nessus Essentials"/>
<br />
<br />


<h3><b>Part 2: Exploring the Search App</b></h3>
<br />

For part 2 I will be exploring the Search App by searching for keywords and also optimizing my search criteria by using specified time periods. <br/>
<br><img src="https://imgur.com/C4rGZw9.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To increase the number of returned events, I adjusted the time frame from Last 24 hours to Yesterday. As displayed below, the amount of events increased from 2,897 to 4,107.<br/>
<br><img src="https://imgur.com/kfGnF3Z.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To run a search with specified relative time ranges I ran a search over the last two days, created the following search query. <br/>
<br><img src="https://imgur.com/Zbmfp9b.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To run a search with specified date and time ranges, I created a custom time time range. For example, to troubleshoot an issue that took place January 6, 2023 about 9:30 AM, I specified the earliest time of 01/06/2024 7:30:00 and the latest time of 01/06/2024 10:30:00 to show the events immediately before and after the issue took place.<br/>
<br><img src="https://imgur.com/ieESetm.png" height="80%" width="80%" alt="Nessus Essentials"/> <br/>
<br/>


<h3><b>Part 3: Searching the Data</b></h3>
<br />

For step 3 I will be creating searches that retrieve events from the index. The data for this lab is for the Buttercup Games online store. The store sells games and other related items, such as t-shirts. In this lab, I will primarily search the Apache web access logs, and correlate the access logs with the vendor sales logs. <br/>
<br>Using the Search Assistant feature, I typed in ‘category’, and selected “categoryid=sports” from the list. <br/>
<br><img src="https://imgur.com/npkGRtI.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/sseoQ8m.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>I then wanted to find out how many errors have occurred on the Buttercup Games website. To retrieve events that mention errors or failures I performed a search using a Boolean operator. Below is a search to retrieve events that contain keywords of buttercupgames and error with a time frame of all time. The Boolean operator, AND was used for this search. <br/>
<br><img src="https://imgur.com/lSjnvnZ.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is a search to retrieve events that contain keywords of error, fail, failure, or severe in the events that also mention buttercupgames. The Boolean operator, OR and the wildcard feature was used for this search. <br/>
<br><img src="https://imgur.com/jv2DpVU.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is an example of a search being performed using fields. Fields are searchable name and value pairings that distinguish one event from another. <br/>
<br><img src="https://imgur.com/uVwhVjN.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is an example of two targeted searches being performed. One is a search for successful purchases from the Buttercup Games store and the other is a search for failed searches. <br/>
<br><img src="https://imgur.com/wURiMjJ.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/0GDpUai.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is an example of a search being performed for errors with a date range of all time. <br/>
<br><img src="https://imgur.com/3JTdP0T.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is an example of a search being performed for a successful purchase of the simulation product for a date range of 1/8/2024 - 1/10/2024.<br/>
<br><img src="https://imgur.com/ufoJTFm.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>I will use the subsearch feature to narrow down the set of events that I search on. The below search is to find the most frequent shopper and the products (productId) that the shopper purchased.  <br/>
<br><img src="https://imgur.com/UvOr8M6.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br />


<h3><b>Part 4: Enabling Field Lookups</b></h3>
<br/>

By enabling the field lookups, I will be able to display the actual product names inside of my searches, dashboards, and reports instead of product codes and product IDs. The first step in the enabling filed lookup process is uploading the file that includes the name of the products that I will like to include in my searches. <br/>
<br><img src="https://imgur.com/qPILMpD.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/mn1mkIc.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/7s1GoNQ.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>When I uploaded the lookup table file, it was uploaded with a default sharing setting as private, so I must change the permissions to the file. For this lab, I am going to share the lookup table file with all applications.<br/>
<br><img src="https://imgur.com/uxfZgUB.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Add the field lookup definition: After the importation of the lookup table files, I must define the information in the lookup table file and how that information relates to the fields in my events, this is called a lookup definition.<br/>
<br><img src="https://imgur.com/dUFiErJ.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/n3TRJcW.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will make the lookup automatic, so instead of using the lookup command in my search when I want to apply a field lookup to your events, the lookup will run automatically.<br/>
<br><img src="https://imgur.com/RxPyRuo.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/6SYtLNn.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will search with the field lookups that were created. As a result of the search, I can see that the both the field lookups that I created were successfully created.<br/>
<br><img src="https://imgur.com/MHMm4Km.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br />


<h3><b>Part 5: Creating Reports and Charts</b></h3>
<br/>

Below I used the search and chart feature to compare the counts of user actions by calculating information about the actions customers have taken on the online store website. This search uses the chart command to count the number of events that are action=purchase and action=addtocart. The search then uses the rename command to rename the fields that appear in the results. The results will show the number of times each product is viewed, the number of times each product is added to the cart and the number of times each product is purchased.<br/>
<br><img src="https://imgur.com/h2DrUhM.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Below is a visualization of the requested data formatted in a column chart.<br/>
<br><img src="https://imgur.com/2ivkF1d.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>I will create a chart that overlays two data series as lines over three data series as columns displayed in an overlay chart. The overlay chart will show Actions such as Adds To Cart and Purchases on one type of chart and the Conversion Rates, such as Views To Purchases, in another type of chart.<br/>
<br>Below is the initial output of the searched data. The x-axis and y-axis was edited to show a better view of the label that describes the data.<br/>
<br><img src="https://imgur.com/XF9IwyS.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will format the second y-axis for the second set of data which is the conversion rates which are viewsToPurchases and cartToPurchase. This will allow the conversion rates now to appear as lines in the chart.<br/>
<br><img src="https://imgur.com/ypwBDNa.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>I then saved the revised chart as a report.<br/>
<br><img src="https://imgur.com/49e8Ggd.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will create a report from a custom chart. In the below example I will create a report that charts which products were purchased over a period of time. <br/>
<br><img src="https://imgur.com/gfMCCtq.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/SwOpjFe.png" height="80%" width="80%" alt="Nessus Essentials"/><br/><br/>
<br>Last, I will create a report from a sparkline chart. This report will show the trends in the number of purchases made over time. The search specifies the purchases made for each product by using categoryId. The search results were then saved as a report. <br/>
<br><img src="https://imgur.com/DVnS8ch.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/hGakijo.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br/>


<h3><b>Part 6: Creating Dashboards</b></h3>
<br/>

To Start the creation of the dashboard, I ran a search for the count of purchases for each product and the percent of each product of the total purchases, then changed the visualization from a bar chart to a pie chart and saved it as a Dashboard Panel. <br/>
<br><img src="https://imgur.com/8rknKop.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/rOaAGwh.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/K97hIpH.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will add controls to the dashboard. Examples of a control include text, a checkbox, or a time range picker. For this example, I am using the time range picker with a three-week date range. With the addition of this control, the inline search that powers the panel now uses the time range that is specified in the shared time picker.<br/>
<br><img src="https://imgur.com/vuFZ85K.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>To include more data inside of the dashboard, I will add additional panels which will consist of the previously saved reports and ad hoc searches.<br/>
<br>This first two panels I will add are from the Purchasing trends and Comparison of Actions and Conversion Rates by Product reports that I previously created.<br/>
<br><img src="https://imgur.com/We4Xc1s.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/S0wgBpr.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/QGtBdZu.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br>Next, I will add a search to the existing dashboard. This search will utilize the productName field from the Enabling Field Lookups section that I previously created. Lastly, I will connect the Top Purchases by Category and VIP Client Purchases panels to the shared Time Range Picker that was configured above. The VIP Client Purchases panel is now connected to the Time range picker input on the dashboard, so when I change the time range on the dashboard, the panels that are connected to the shared Time Range Picker are all updated. The dashboard is now completed.<br/>
<br><img src="https://imgur.com/h9OPRYZ.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br><img src="https://imgur.com/upgfmbg.png" height="80%" width="80%" alt="Nessus Essentials"/><br/>
<br />
<br />
</p>
