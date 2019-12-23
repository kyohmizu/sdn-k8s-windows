# SDN-k8s-Windows

Forked from https://github.com/microsoft/SDN/tree/master/Kubernetes/windows

These are custom scripts for joining windows server nodes to a kubernetes cluster that is created with [Hard Way on Azure](https://github.com/ivanfioravanti/kubernetes-the-hard-way-on-azure).

# Usage

Before running scripts on windows server nodes, you need to run the commands below.

```powershell
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
Install-Package -Name Docker -ProviderName DockerMsftProvider
Restart-Computer -Force

# Restart a machine

docker pull mcr.microsoft.com/windows/nanoserver:1809
docker tag mcr.microsoft.com/windows/nanoserver:1809 mcr.microsoft.com/windows/nanoserver:latest

mkdir c:\k
cd c:\k
```

After that, you need to prepare kubeconfig and kubernetes node binaries in `c:\k`.

```powershell
ls config,*exe

    Directory: C:\k

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       12/22/2019  11:49 AM           6254 config
-a----       12/11/2019   1:14 PM       40086016 kube-proxy.exe
-a----       12/11/2019   1:20 PM       47195136 kubectl.exe
-a----       12/11/2019   1:20 PM      119127552 kubelet.exe
```

Then download the scrips in this repository in the same directory.
And run the command below.

```powershell
.\start.ps1 -masterIp [private IP of the node] -clusterCIDR 10.200.0.0/16
```