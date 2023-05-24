```powershell
#Get Graph API Intune Module
Install-Module NuGet
Install-Module -Name Microsoft.Graph.Intune
Import-Module Microsoft.Graph.Intune -Global

#The path where the scripts will be saved
$Path = “C:\temp”

#The connection to Azure Graph
Connect-MSGraph
$Main_Path = “https://graph.microsoft.com/beta/deviceManagement/deviceHealthScripts”

#Get Graph scripts
$List_All_Scripts = (Invoke-MSGraphRequest -Url $Main_Path -HttpMethod Get).value
$List_All_Scripts | out-gridview
```

- (https://call4cloud.nl/2021/05/the-laps-reloaded/)[https://call4cloud.nl/2021/05/the-laps-reloaded/] 
- (https://call4cloud.nl/2022/01/proactive-remediatons-the-hidden-world/)[https://call4cloud.nl/2022/01/proactive-remediatons-the-hidden-world/]
- (https://github.com/j0eyv/ProactiveRemediations)[https://github.com/j0eyv/ProactiveRemediations]
- (https://www.joeyverlinden.com/my-most-used-proactive-remediations/#htoc-detect-adobedc-java-ps1)[https://www.joeyverlinden.com/my-most-used-proactive-remediations/#htoc-detect-adobedc-java-ps1]
