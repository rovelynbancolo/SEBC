HDFS Lab: Test HDFS Snapshots:

Create a precious directory in HDFS; copy the ZIP course file into it.

#sudo -u hdfs hdfs dfs -mkdir /user/precious
#sudo -u hdfs hdfs dfs -chown precious: /user/precious
Placed the SEBC.zip file to /precious directory
   #useradd precious
   --> Add a new user name precious in HUE and upload the SEBC file.

HDFS -> FileBrowser -> Enable Snapshot -> Navigate through /user/Precious directory -> Enable Snapshot

snapshot -> sebc-hdfs-test

Delete the SEBC file

	#hdfs dfs -rm /user/precious/SE*
	  Delete the precious dir.
	  rmr: Failed to move to trash: hdfs://ip-172-31-3-221.ap-southeast-1.compute.internal:8020/user/precious: The directory /user/precious cannot be deleted since /user/precious is snapshottable and already has snapshots

Restore the the deleted file

	Click on the arrow down after /user/precious.
	Restore directory from a SnapShot.
	Select Use the HDFS 'copy' command.
	Restore