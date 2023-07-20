#knowledgebase  #Datto #restore #V2

# How to restore files from a Datto Appliance

Note: this was written for a customer who has local access to their Datto appliance enabled. Local Access to the Datto would need to be enabled in the partner portal for these instructions to be accurate.

Log into the Datto webpage with your local Datto admin credentials. For instance, open [https://192.168.5.50](https://192.168.5.50) in a web browser. 

In the top ribbon, click on the RESTORE button. You will need to first choose your system, then the recovery type. As you can see in the screenshot below there are only 1 option for each of these. Under “Choose a Recovery Point” click the dropdown and choose the time that you want to recover the files from. Once you have selected the time click Start Restore.

After a few moments the Recovery Point will be available to mount. Click the Mount button to be able to explore the backup.

Once the recovery point is mounted click on the Access Web Share link, or use the SMB link to drag and drop the files to the source. The SMB link may be the better option, especially for restores with large amounts of data. 

This will open a file recovery window. Browse to the files that you want to recover. You can click on an individual file to download it, or click on the icon to the left of a folder to download the whole folder as a .zip file. Once you have recovered the files that you need, click on the Unmount button to end the restore session.
