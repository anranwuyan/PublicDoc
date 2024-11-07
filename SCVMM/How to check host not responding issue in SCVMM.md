Some general commands to narrow down host not responding issue in SCVMM.

1. refresh the host in SCVMM , and then to check the error details in the job

   
2. check the error details in the properties of the host in VMM.

   
3. run below commands to check the winrm connections between the vmm and the host

--check vmm agent version
Invoke-WmiMethod -Class AgentManagement -Name GetVersion -Namespace "root\scvmm" -ComputerName "HYPERV1912" 

--get winrm config of the host

winrm get winrm/config -r:Hostname

winrm id -r:fqdn

enter-pssession -computername 'hostname of hyper v' 


--some other general used wmi queries 
Get-WmiObject -Namespace "root\virtualization\v2" -Class Msvm_ComputerSystem -ComputerName 'FQDN'

Invoke-WmiMethod -Class AgentManagement -Name GetVersion -Namespace "root\scvmm" -ComputerName FQDN


get-wsmaninstance -computername "HostFQDN" -resourceuri "http://schemas.microsoft.com/wbem/wsman/1/wmi/root/cimv2/win32_operatingsystem"


Get-CimClass -Namespace root/virtualization/v2 -classname *vmm*

Get-WmiObject -Namespace "root\mscluster" -class "MSCluster_Service" -ComputerName "clustername"

3. compare the winrm setting with a working node, or with scvmm, and apply the same setting on the problematic node, also engage WINRM team if needed.

winrm get winrm/config -r:Hostname


4. enable credssp if needed.


        winrm set winrm/config/service/auth @{CredSSP="True"}

     winrm set winrm/config/winrs @{AllowRemoteShellAccess="True"}

     winrm set winrm/config/winrs @{MaxMemoryPerShellMB="2048"}

     winrm set winrm/config/client @{TrustedHosts="*"}

     winrm set winrm/config/client/auth @{CredSSP="True"}
   














