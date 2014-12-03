generate-and-delivery-ssh-keys
====

Assumption
----
You are running or have the following:
- A centralized authentication LDAP/AD
- ldapsearch is installed on your rundeck server(s)
- Google Apps Business with a service account credentials with the ability to upload to anyone's drive company wide
- Gitlab server: user with admin token

The idea
----
When using tools like Github or Gitlab in a windows environment, some engineers and/or developers don't have the ability to generate an SSH key.  This job provides a way to generate an SSH key on a trusted system and deliver it securely to a private location.  It will even takt the step of uploading it (currenly only Gitlab but Github API is similar so addition or adaptation should be easy enough) to your git profile if so desired.

What the current scripts do
----
1. Bash: queries the user email address from your cental auth server with ldapsearch (because email addresses appear to be managed in rundeck instead of populated like most appplications).  It gerneates and SSH key and stores it in a standard location with a standar format.  (To allow use by other scripts)
2. Ruby: Authentiates with Google and delivers the packaged SSH keys to the users Google Drive (identifed by email address) in a folder named in the rundeck job.
3. Ruby: If user has selected in the job to upload to Gitlab, it will send the SSH key to the user profile through the API
4. Bash: cleanup

TODO
----
- add error handlers to undo any successful steps and rollback on failure
