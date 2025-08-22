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
<img src="https://imgur.com/FvvvxTb.png" alt="Azurelogo"/>
</p>
<br />
1. enable Insights on the VM. Click on your VM on the left menu click monittoring > Insights > Click enable
Refresh and you shoudd be sble to see performance charts.
 Once that’s there you’ll have access to Memory and Disk metrics in Metrics/Alerts.
 </p>
<br />
<img src="https://imgur.com/cEBRkSy.png" alt="Azurelogo"/>
</p>
<br />
2. Search up log analytics workspace and create one for your selected VM.
Make sure it has the same resource group and region as your VM!!
Then go to go to your VM → Extensions + applications. THe AzureMonitorWindowsAgent (AMA) extension should be installed. Azure can already track the CPU from the host but for tracking the disk and memory we will need the AMA ext.
</p>
<br />
3. The next step would be to create alerts for the CPU. We will do the  Disk and Memory afterwwards.
In the Azure Portal, go to your VM.
On the left menu, under Monitoring, click Alerts.
Click Create >Alert rule.
</p>
<br />
<img src="https://imgur.com/non2LxA.png" alt="Metrics"/>
</p>
<br />
4. In the condition tab:
    Signal name: Percentage CPU
    Value is: Greater than
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
Make sure the subscription and resource group you want is selected.
Create an Action Group name and Display Name.
</p>
<br />
6. Now go to the Notifications Tab
For notif type select: Email/SMS/Push/Voice
Enter whichever way of contact you prefer and name the alert CPU. Click Create ahd you should recieve a notif from Azure.
</p>
<br />
<img src="https://imgur.com/5XSkCYH.png" alt="Azurelogo"/>
</p>
<br />
7. Stay within the rule creation tab and go to details. and choose your severity level from level 4 (low) to zero (critical).
</p>
<br />
</p>
<br />
8. Now we will set up monitoring for the disk next. Azure can already track the CPU from the host but for tracking the disk and memory we will need
to set up the Azure Monitor Agent (AMA). 
</p>
<br />
9.





