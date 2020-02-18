# Role Name:
- ansible-role-event-log-archiver-zip-move-to-ibmeventlogs-folder

# Description:
This role will check the server's drives (C, D, E, & F), at the root level, for
a directory called ibmeventlogs.   If none are found then a folder will be
created on the C: drive called c:\\ibmeventlogs.   The role will also ensure
that the necessary ZIP utility file is on the server.  The role will then zip
the system, security and application event logs files (archive*.evtx) inside the
previously mentioned folder called ibmeventlogs.   Once the files are zipped,
then the playbook will remove the archive*.evtx files.

# Requirements
Windows Ansible related pre-requisites

# Role Variables:
# Defaults file-ansible-role-event-log-archiver-zip-move-to-ibmeventlogs-folder

Parameter | Choices/Defaults|Comments
----------|-----------------|--------
__zip_path__  (string)|"C:\\Scripts\\Sec_Log_Archive\\7z"|default zip path
__windows_default_log_path__ (string)|"C:\\windows\\system32\\winevt\\logs"|default log path
__number_days_before_deletion__ |270|# of days old before it will delete file

# Results from execution

Return Code | Success of execution| effect on target machine | Comments
----------|-----------------|--------|---------
0 | True | True | event log manager on __affected_host__  was successful.
0 | True | False | event log manager on  __affected_host__ took no action.
3000 | False | False | could not find or create the ibmeventlogs folder.
3001 | False | False | could not find the zip_path folder and executable.


# Example Playbook:
---
 - hosts: [win]
   roles:
   - ansible-role-event-log-archiver-zip-move-to-ibmeventlogs-folder


# Author Information:
Richard M. Williams (rmwill@us.ibm.com)
