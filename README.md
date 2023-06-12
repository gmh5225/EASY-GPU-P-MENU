# UPDATE!
A new version is finally coming, I'm currently developing a new menu for hyper-v in general that will replace this menu...
Stay tuned and thank you for your support!

# Easy-GPU-P with an integrated menu!
Fork Of The Original Easy-GPU-PV, With a menu!

## Guide:
1. Download the menu from this link: https://github.com/codygamer666/EASY-GPU-P-MENU/releases 
2. Drop the Win10/11 ISO in the iso folder and rename it WIN.iso
3. Run menu.ps1 and follow the options

## Features:
1. Creates a new vm with gpu-p, drivers and parsec using hyper-v
2. Adds Gpu-p to an existing vm, including drivers
3. Updates a gpu-p vm drivers
4. Run the PreChecks script
5. Remove gpu-p adapter from vm
6. Print A List Of Available GPUS In Your System (Even On Laptops Yea)

You can find the original Repo at: https://github.com/jamesstringerparsec/Easy-GPU-PV

All Credits to @jamesstringerparsec

![beta1](https://user-images.githubusercontent.com/96527590/149619581-df924e1a-b753-477c-a17d-76af0ff2318c.JPG)

## Restore VMGpuPartitionAdapter
```batch
Remove-VMGpuPartitionAdapter -VMName $yourvmname -ErrorAction SilentlyContinue
```
## Restore EnhancedSessionMode
```batch
Set-VMHost -EnableEnhancedSessionMode $True
```
## Enable/Disable Nested Virtualization
```batch
Set-VMProcessor -VMName $yourvmname -ExposeVirtualizationExtensions $true
Set-VMProcessor -VMName $yourvmname -ExposeVirtualizationExtensions $false
```

## Documents
- https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/nested-virtualization
- https://github.com/HyperDbg/HyperDbg/issues/135

## Manual Setting
```
$vm = "vm-name"
Add-VMGpuPartitionAdapter -VMName $vm
Set-VMGpuPartitionAdapter -VMName $vm -MinPartitionVRAM 80000000 -MaxPartitionVRAM 100000000 -OptimalPartitionVRAM 100000000 -MinPartitionEncode 80000000 -MaxPartitionEncode 100000000 -OptimalPartitionEncode 100000000 -MinPartitionDecode 80000000 -MaxPartitionDecode 100000000 -OptimalPartitionDecode 100000000 -MinPartitionCompute 80000000 -MaxPartitionCompute 100000000 -OptimalPartitionCompute 100000000

Set-VM -GuestControlledCacheTypes $true -VMName $vm
Set-VM -LowMemoryMappedIoSpace 1Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 32GB –VMName $vm
```
## Dll Migration
On your host machine, go to `C:\Windows\System32\DriverStore\FileRepository\`
and copy the `nv_dispi.inf_amd64` folder to `C:\Windows\System32\HostDriverStore\FileRepository\` on your VM (This folder will not exist, so make sure to create it)
Next you will need to copy 

`C:\Windows\System32\nvapi64.dll` file from your host to `C:\Windows\System32\` on your VM

`C:\Windows\SysWow64\nvapi.dll` file from your host to `C:\Windows\SysWow64\` on your VM

And once that is done, you can restart the VM.

## About the slowdown of the Hyper-V virtual machine network
The host computer is connected to the WIFI network. I tried to change the adapter option in the network and Internet to find the WLAN (this is if the name is not changed), right-click to open the properties, find the configuration under the network card name, select the advanced tab, find the preferred frequency band and change it to the preferred 5GHz/6Ghz frequency band. save.
