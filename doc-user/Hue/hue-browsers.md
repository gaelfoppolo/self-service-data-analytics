# Browsers

------

The browsers in hue provide a fluid and friendly data navigation. There are several types of browsers. We will see them all in this document.



## Table

------

The table browser allow you to manage the databases, tables and partitions of the metastore shared by Hive and Impala. Through the browser you can do the following :

- Select, create or drop databases
- Tables
  - Create, browse or drop tables
  - Browse table data and metadata
  - Import data into a table
  - Filter, sort and browse partitions



## Files

------

The file browser allow you to manipulate the files in HDFS. With you can do the following :

- Create files and directories, upload and download files, upload zip archives, and rename, move, and delete files and directories. You can also change a file's or directory's owner, group, and permissions
- Search for files, directories, owners, and groups
- View and edit files as text or binary

### Files and directories

You can use File Browser to view the input and output files of your MapReduce jobs. You could for example save your output files in /tmp or in your home directory. You must have the proper permissions to manipulate other user's files.

#### Creating Directories

1. In the File Browser window, select **New > Directory**.
2. In the **Create Directory** dialog box, enter a directory name and then click **Submit**

#### Changing Directories

- Click the directory name or parent directory dots in the **File Browser** window.
- Click the ![image](http://cloudera.github.io/hue/latest/user-guide/images/edit.png) icon, type a directory name, and press **Enter**.

#### Creating Files

1. In the File Browser window, select **New > File**.
2. In the **Create File** dialog box, enter a file name and then click **Submit**.

#### Uploading Files

You can upload text and binary files to the HDFS.

1. In the **File Browser** window, browse to the directory where you want to upload the file.
2. Select **Upload > Files**.
3. In the box that opens, click **Upload a File** to browse to and select the file(s) you want to upload, and then click **Open**.

#### Downloading Files

You can download text and binary files to the HDFS.

1. In the **File Browser** window, check the checkbox next to the file you want to download.
2. Click the **Download** button.

### Uploading Zip Archives

You can extract zip archives to the HDFS. The archive is extracted to a directory named archivename.

1. In the **File Browser** window, browse to the directory where you want to upload the archive.
2. Select **Upload > Zip file**.
3. In the box that opens, click **Upload a zip file** to browse to and select the archive you want to upload, and then click **Open**.

### Trash Folder

File Browser supports the HDFS trash folder (*home directory*/.Trash) to contain files and directories before they are permanently deleted. Files in the folder have the full path of the deleted files (in order to be able to restore them if needed) and checkpoints. The length of time a file or directory stays in the trash depends on HDFS properties.

In the **File Browser** window, click ![image](http://cloudera.github.io/hue/latest/user-guide/images/fbtrash.png).

### Changing Owner, Group, or Permissions

Only the Hadoop superuser can change a file's or directory's owner, group, or permissions. The user who starts Hadoop is the Hadoop superuser. The Hadoop superuser account is not necessarily the same as a Hue superuser account. If you create a Hue user (in User Admin) with the same user name and password as the Hadoop superuser, then that Hue user can change a file's or directory's owner, group, or permissions.

**Owner or Group**

1. In the **File Browser** window, check the checkbox next to the select the file or directory whose owner or group you want to change.

2. Choose **Change Owner/Group** from the Options menu.

3. In the

    

   Change Owner/Group dialog box:

   - Choose the new user from the **User** drop-down menu.
   - Choose the new group from the **Group** drop-down menu.
   - Check the **Recursive** checkbox to propagate the change.

4. Click **Submit** to make the changes.

**Permissions**

1. In the **File Browser** window, check the checkbox next to the file or directory whose permissions you want to change.
2. Click the **Change Permissions** button.
3. In the **Change Permissions** dialog box, select the permissions you want to assign and then click **Submit**.

### Viewing and Editing Files

You can view and edit files as text or binary.

**View**

1. In the File Browser window, click the file you want to view. File Browser displays the first 4,096 bytes of the file in the File Viewer window.
   - If the file is larger than 4,096 bytes, use the Block navigation buttons (First Block, Previous Block, Next Block, Last Block) to scroll through the file block by block. The **Viewing Bytes** fields show the range of bytes you are currently viewing.
   - To switch the view from text to binary, click **View as Binary** to view a hex dump.
   - To switch the view from binary to text, click **View as Text**.

**Edit**

1. If you are viewing a text file, click **Edit File**. File Browser displays the contents of the file in the **File Editor** window.
2. Edit the file and then click **Save** or **Save As** to save the file



## Jobs

------

The Job Browser application lets you to examine multiple types of jobs jobs running in the cluster. Job Browser presents the job and tasks in layers. 
The top layer is a list of jobs, and you can link to a list of that job's tasks. You can then view a task's attempts and the properties of each attempt, such as state, start and end time, and output size. 
To troubleshoot failed jobs, you can also view the logs of each attempt.
If there are jobs running, then the Job Browser list appears.

### Viewing job information

**To view job information for an individual job:**

1. In the **Job Browser** window, click **View** at the right of the job you want to view. This shows the **Job** page for the job, with the recent tasks associated with the job are displayed in the **Tasks** tab.
2. Click the **Metadata** tab to view the metadata for this job.
3. Click the **Counters** tab to view the counter metrics for the job.

**To view details about the tasks associated with the job:**

1. In the **Job** window, click the **View All Tasks** link at the right just above the **Recent Tasks** list. This lists all the tasks associated with the job.
2. Click **Attempts** to the right of a task to view the attempts for that task.

**To view information about an individual task:**

1. In the **Job** window, click the **View** link to the right of the task. The attempts associated with the task are displayed.
2. Click the **Metadata** tab to view metadata for this task. The metadata associated with the task is displayed.
3. To view the Hadoop counters for a task, click the **Counters** tab. The counters associated with the task are displayed.
4. To return to the **Job** window for this job, click the job number in the status panel at the left of the window.

**To view details about a task attempt:**

1. In the **Job Task** window, click the **View** link to the right of the task attempt. The metadata associated with the attempt is displayed under the **Metadata** tab.
2. To view the Hadoop counters for the task attempt, click the **Counters** tab. The counters associated with the attempt are displayed.
3. To view the logs associated with the task attempt, click the **Logs** tab. The logs associated with the task attempt are displayed.
4. To return to the list of tasks for the current job, click the task number in the status panel at the left of the window

