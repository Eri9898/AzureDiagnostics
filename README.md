# AzureDiagnostics
How to monitor your online environment
<p align="center">
<img src="https://imgur.com/IrEGWDd.png" alt="Azurelogo"/>
</p>

<h1>AzureDiagnostics</h1>
How to monitor your online environment <br />
</p>
<br />
<h2>Azure Monitor Metrics + Alerts </h2>
</p>
<br />
<img src="https://imgur.com/bWyM5m1.png" alt="Azurelogo"/>
</p>
<br />
1. We will be creating alerts for the CPU< memory, and disks. So go to your VM and head into Monitoring> Metrics.
  </p>
<br />
<img src="https://imgur.com/6s9xfvz.png" alt="Metrics"/>
</p>
<br />
2. Next you will set up your metric chart. 
  Scope: Your VM
  Metric namespace: pick Virtual Machine Host
  Metric: pick Percentage CPU
  CREATE
</p>
<br />
3. Now that your CPU metric chart is created, you will be adding an alert to go with it! So above the metric tab, click on the alerts tab. 
</p>
<br />
<img src="https://imgur.com/HK096qu.png" alt="CreateAlert"/>
</p>
<br />
4. Click create at the top then alert rule.
Pick Percentage CPU metric again.
In the condition tab:
    Signal name: Percentage CPU
    Vale is: Greater than
    Threshold: 80%
    Look back period: 5 minutes
    Check every: 1 minute
</p>
<br />
<img src="https://imgur.com/LYb1J8J.png" alt="CreateAction"/>
</p>
<br />
5. Next go to the Actions tab. 
Next to Select Actions, select Use Action Groups.
Then click create Action Group at the top.
Make syr the subscription and resource group you want is selected.
Create an Action Group name and Display Name.
</p>
<br />
6. Now go to the Notifications Tab
For notif type select: Email/SMS/Push/Voice
Enter whicheverway of contact you prefer and name the alert CPU. Click Create ahd you should recieve a notif from Azure.
</p>
<br />
<img src="https://imgur.com/aFCNhZH.png" alt="Azurelogo"/>
</p>
<br />
7. Stay within the rule creation tab and go to details. and choose your severity level from level 4 (low) to zero (critical).
</p>
<br />
8. Now it's time to test the alert! RDP into your VM and open command line.
</p>
<br />
9. Now we will set up monitoring for the disk and memory. Azure can already track the CPU from the host but for tracking the disk and memory we will need
to set up the Azure Monitor Agent (AMA). 
</p>
<br />
<img src="https://imgur.com/aFCNhZH.png" alt="Azurelogo"/>
</p>
<br />
10. So before doing that, you will have to create a log analyticss workspace.
so search it up in Azure. Select your subscription and make sure it has the same resource group and region as your VM.
</p>
<br />
11. Now install the AMA. So go back to your VM, on the left menu go to settings > Extensions + Applications.





