# AzureDiagnostics
How to monitor your online environment
<p align="center">
<img src="https://imgur.com/IrEGWDd.png" alt="Azurelogo"/>
</p>

<h1>AzureDiagnostics</h1>
This tutorial demonstrates setting up Azure Monitor with actionable alerts (CPU, Memory, Disk) on a Windows Server VM, including stress-testing to verify alert functionality. <br />
</p>
<br />
<h2>Azure Monitor Metrics + Alerts </h2>
</p>
<br />
<img src="https://imgur.com/FvvvxTb.png" alt="Azurelogo"/>
</p>
<br />
1. enable Insights on the VM. Click on your VM on the left menu click monitoring > Insights > Click enable
Refresh and you shoudd be sble to see performance charts.
 Once that’s there you’ll have access to Memory and Disk metrics in Metrics/Alerts.
 </p>
<br />
<img src="https://imgur.com/cEBRkSy.png" alt="Azurelogo"/>
</p>
<br />
2. Search up log analytics workspace and create one for your selected VM.
Make sure it has the same resource group and region as your VM!!
Then go to go to your VM > Extensions + applications. The Azure Monitor Windows Agent (AMA) extension should be installed. Azure can already track the CPU from the host but for tracking the disk and memory we will need the AMA ext.
</p>
<br />
3. The next step would be to create alerts for the CPU. We will do the Disk and Memory afterwards.
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
Enter whichever way of contact you prefer and name the alert CPU. Click Create and you should recieve a notif from Azure.
</p>
<br />
<img src="https://imgur.com/5XSkCYH.png" alt="Azurelogo"/>
</p>
<br />
7. Stay within the rule creation tab and go to details. Choose your severity level from level 4 (low) to zero (critical).
</p>
<br />
8. Now we will set up monitoring for the memory next. Go to alerts again> create> alert rule.
next. 
</p>
<br />
<img src="https://imgur.com/tPd2BzJ.png" alt="Azurelogo"/>
</p>
<br />
9. In the scope tab make sure your VM is selected and you have the correct resource group selected. Then in the condition tab your
signal : Available Memory Percentage
Value is: Less than
Threshold: 20%
Check every: 1 min
Loopback period: 5 mins
</p>
<br />
10. Go to the actions tab and add it to the same action group as your other alert. And give the alert a name which would be "memory". Then select your notif type. Then  in the details tab select your severity, and alert rule name. Then review and create!
</p>
<br />
11. Now we will set up an alert for the disk. So once more go to monitoring> alerts> create> alert rule. In the condition tab
Signal type: VM Free Disk Space
Operator: Less than
Threshold value: 10%
Freq of evaluation: 5 mina
</p>
<br />
12. In the actions tab select the same action group, notification type and select an alert name.
</p>
<br />
13. In the detail tab select critical severity, name your alert "disk". Then review and create
</p>
<br />
14. You should have three alerts that monitor:
    CPU over 80% (spikes)
    Memory under 20% (running low)
    Disk free space under 10% (almost full)
    and it's time to test if they work!
</p>
<br />
<img src="https://imgur.com/aWgunBF.png" alt="Azurelogo"/>
</p>
<br />
15. First let's test the CPU. Remote Desktop (RDP) into your VM.
Open PowerShell as Administrator.
Paste this command to max out CPU:
Start-Job { while ($true) { [Math]::Sqrt(12345) } }
</p>
<br />
16. This runs an infinite loop doing math. Open Task Manager and watch CPU skyrocket to 80–100%.
</p>
<br />
17. Leave it running for about 10 minutes so Azure metrics can collect it.
Check Azure Alerts and You should see HighCPU fire
</p>
<br />
<img src="https://imgur.com/6RkFJfy.png" alt="Azurelogo"/>
</p>
<br />
18. Stop the CPU with:
Get-Job | Stop-Job | Remove-Job
</p>
<br />
<img src="https://imgur.com/5WOzIgE.png" alt="Azurelogo"/>
</p>
<br />
19. Now we will test memory. So open command line again as an admin and paste this:
$a = @()
for ($i=0; $i -lt 100000; $i++) {
    $a += New-Object Byte[] (10MB)
}
</p>
<br />
20.  This slowly eats up memory.
Watch Task Manager, Memory climbs until it passes your threshold (below 20% free).
</p>
<br />
21. After a few minutes the low memory alert should fire.
</p>
<br />
22. To stop simply restart the VM. 
</p>
<br />
23. Now we will test the disk. So create a temp fie named in your local drive called "Temp"
</p>
<br />
<img src="https://imgur.com/YUvWn3D.png" alt="Azurelogo"/>
</p>
<br />
24. Run this in Command Line
fsutil file createnew C:\temp\bigfile.txt 5000000000
</p>
<br />
<img src="https://imgur.com/pRS3h7w.png" alt="Azurelogo"/>
</p>
<br />
25. This  Creates a 5GB dummy file instantly. Repeat until disk space < 10%. Azure should trigger LowDiskSpace.
</p>
<br />
26. Cleanup: Delete those dummy files with:
    Remove-Item C:\temp\bigfile.txt
  </p>
<br />
Setting up and testing alerts proactively is a key monitoring responsibility in any kind of environment.


    










