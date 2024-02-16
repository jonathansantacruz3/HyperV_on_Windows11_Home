
![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/7c69054c-b9fc-4ef4-a7bb-245bebaeeaf0)



<h1>Hyper-V on Windows 11 Home Edition</h1>
This tutorial showcases the process and installation of the Hyper-V manager for virtual machines onto Windows 11 Home Edition. I review restore points and why you should use them on your system. I also exhibit the power of batch scripting to enable the Hyper-V feature without the need to upgrade to the Pro edition.  Home has many of the features that Pro has with a few key distinctions. Security, virtualization, and power limitations are what set these editions apart. In my own system I run a Windows 11 Home Edition on a MSI gaming laptop with an 11th-generation Intel i7 CPU processor. 

<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Restore Point 
- Notepad
- Command Prompt
- Microsoft Hyper V (Virtual Machines/Compute)

<h2>Operating Systems Used </h2>

- Windows 11 Home Edition </b> (23H2)

<h2>List of Prerequisites</h2>

- Enable BIOS Virtualization 
- Create System Restore Point 
- Save Script as Batch File & Open File as Administrator 
- Restart Computer to Finish Installation
- Verify Hyper-V is installed 


<h2>Installation Steps</h2>

<h3>Enable BIOS Virtualization</h3>

Before you try anything you want to make sure that you ensure that virtualization is enabled in the BIOS. Every computer varies on how to get into the BIOS and configure this so check with your manufacturer to set this correctly. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/9a536957-eb36-4274-a16b-4de71cd262d8)

One way you can verify that virtualization is enabled is to open up your Task Manager and under the performance tab locate CPU and it should display enabled. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/c0b5d417-5556-4088-b4c9-9e3b0744fa3b)


<h3>Create System Restore Point</h3>

The next thing you want to do before any major changes are made to your computer is to create a safety net with a restore point. A restore point acts as a checkpoint to revert back to that point in time in case anything goes wrong after an update or application installation. It copies all files in the desired drive to be able to create the restore point. 300 Mb of drive space is required for this step and another thing worth mentioning is if you do restore your computer to that checkpoint it will not restore personal files such as email, documents, or media within the timeframe of the checkpoint to the restoration point. 

In the search bar, type in "create a restore point". Click on the System Protection tab and it should display the window below. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/ea15ef5f-a3da-4ea3-b392-d9cd8fe7b888)

Select the desired drive to create the restore point and choose the "Configure" button if protection is off. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/eb864b00-de1a-424a-9d7f-62336abe4037)

Make sure to turn on protection and set the marker to the desired disk space protection. I set mine to 2% which totals to 9.08 Gb. Once you select "Apply" and "OK" choose "Create" to create your restore point. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/9128c0ab-05ae-4479-8a4c-349eaf2ef2ef)

Name it something that corresponds to what you are working on. In my case, I named mine "pre-hyperV". 

<h3>Copy of Batch Script & Save Script as Batch File & Run as Administrator</h3>

The Script:

pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL
pause


Batch scripting is a set of commands executed through the command prompt with elevated permissions and automates tasks to make configuration and installation easier. First, open up notepad and copy the script. The script will be stored in a file with the .bat extension and under file types, choose All Files *.*. You will then locate the file and run it as administrator to start automating the commands and enable Hyper-V. For those of you that want a description of what the script is doing line by line I will include it below. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/249d5049-46d5-4fbf-8980-c2b0057fadea)

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/6f27f917-1a86-49e8-a9be-9a2e1e6b95ef)

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/7ac18606-a359-4235-8738-29219f8acd78)

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/5e4c05ff-ab98-48d4-95eb-bfb5316c2ade)



<h3></h3>

<h3>Restart Computer to Finish Installation</h3>

Once the script has run its course on the command prompt, restart the computer by typing "YES" on the command prompt after it asks you if you want to restart now. 

<h3>Verify Hyper-V is installed </h3>

If all goes well you should be able to locate Hyper-V in the search bar. If it is not there, search control panel and choose "Programs and Features". 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/a59d7994-8bd7-423b-a469-e4893d6b04e9)

Choose the "Turn Windows Features on or off" in the left panel side. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/4a1db02e-5b01-4c79-b786-5ffe1bf95a48)

Locate the Hyper-V option and check it. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/5e15a76d-94a4-4966-ac2f-2996def416fb)

After pressing "OK", the feature will load and you will be able to run Hyper-V on your Windows Home Edition computer with no upgrades. 

![image](https://github.com/jonathansantacruz3/HyperV_on_Windows11_Home/assets/151465848/305632e9-fdd7-4998-8587-120106884e99)

I was thrilled to be able to use this feature and use it as a base for my home lab projects. I hope it will give you the same pleasure. 
