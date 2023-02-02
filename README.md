
|**#**|**Task names**|**Command steps and outputs**|
| :-: | :-: | :-: |
|**1**|<p></p><p></p><p>**In this step we download NFS kernel server in the ubuntu server side.**</p><p></p>|<p>*#sudo apt install nfs-kernel-server*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.002.png)</p><p></p>|
|**2**|**Firstly, we will create a directory named “sharedFile” that is going to be shared by client system.**|<p>*#sudo mkdir –p /mnt/nfs/sharedFile*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.003.png)</p><p></p>|
|**3**|**Next, set the permissions of the created “sharedFile” directory so that all client machines can easily access it.**|<p>*#sudo chown -R nobody:nogroup /mnt/nfs/sharedFile*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.004.png)</p><p></p><p></p>|
|**4**|**Set the file permissions as required. In our case, we have allocated the read, write, and execute permissions to the “sharedFile” directory files.**|<p>*#sudo chmod 777 /mnt/nfs/sharedFile*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.005.png)</p><p></p>|
|**5**|**In this step, we will grant access to the client system for accessing the NFS server. To do so, open “/etc/exports” in the “nano” editor.**|<p>*#sudo nano /etc/exports*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.006.png)</p><p></p>|
|**6**|**We will permit an entire subnet “192.168.127.128” to access the NFS server.**|<p>*# /mnt/nfs/sharedFile 192.168.127.128/24(rw,sync,no\_subtree\_check)*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.007.png)</p><p></p>|
|**7**|**Utilize the provided command for exporting the NFS shared directory.**|<p>*#sudo exportfs -a*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.008.png)</p><p></p>|
|**8**|<p>**Restart NFS server.**</p><p></p>|<p>*#sudo systemctl restart nfs-kernel-server*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.009.png)</p><p></p><p></p>|
|**9**|**Next, grant the Firewall access to the client system.**|<p>*#sudo ufw allow from 192.168.127.128/24 to any port nfs*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.010.png)</p><p></p><p></p>|
|**10**|**Enable Firewall**|<p>*#sudo ufw enable*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.011.png)</p><p></p><p></p>|
|**11**|**Next, verify that the Firewall is configured to allow the access through the port “2049”**|<p>*#sudo ufw status*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.012.png)</p><p></p><p></p>|
|**12**|**Installing NFS client on Ubuntu**|<p>*#sudo apt install nfs-common*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.013.png)</p><p></p>|
|**13**|**We will test the access co-ordination between NFS server. We create a mount point on the NFS client system**|<p>*#sudo mkdir -p /mnt/nfs/sharedFileClient*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.014.png)</p><p></p>|
|**14**|**Mount the NFS share on the other Client system**|<p>*#sudo mount 192.168.127.129:/mnt/nfs/sharedFile /mnt/nfs/sharedFileClient*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.015.png)</p><p></p>|
|**15**|**For the testing NFS share on the client system, firstly we create some files in the “sharedFile” directory on the “asimserver” NFS server**|<p>*# cd /mnt/nfs/sharedFile*</p><p>*# touch test{1..10}*</p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.016.png)</p><p></p><p></p><p></p>|
|**16**|**Then, switch to the client system and view the list of files which we create on “asimsever”.**|<p>*#ls -l /mnt/nfs/sharedFileClient*</p><p></p><p>![](Aspose.Words.8f984bc6-7729-405f-a6cf-6b8c34f82e0d.017.png)</p><p></p>|

