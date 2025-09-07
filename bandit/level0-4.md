# 🔹 Bandit Notes | Levels 0–4

---

## 🔹 Level 0 → 1

**Challenge:** Log into the server via SSH.

**Solution Command:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220

Step-by-Step Explanation:

SSH (Secure Shell) allows encrypted remote login.

-p 2220 specifies a non-default port.


Real-World Scenario:

> Misconfigured SSH or default credentials are a common attack vector.
Example: In 2021, attackers used weak SSH passwords to compromise servers and mine crypto (CSO Online).



Teaching Points:

Always verify open ports (nmap -p 2220 <host>).

Never leave default passwords.

Key-based authentication is more secure than passwords.


Defense / Mitigation:

Disable password login; use key-based authentication.

Change default SSH port.

Limit access to specific IPs and enable 2FA.



---

🔹 Level 1 → 2

Challenge: Read a file named -.

Solution Command:

cat ./-

Step-by-Step Explanation:

The file is named -, normally interpreted as standard input.

Using ./- forces the shell to treat it as a filename.


Real-World Scenario:

> Attackers exploit special filenames in uploads to bypass validation.
Example: CVE-2017-5638 (Apache Struts) used improper handling of input filenames/headers to achieve remote code execution (CVE MITRE).



Teaching Points:

Learn how special characters affect shell commands.

Use quoting ("./-") or escaping when handling unusual filenames.


Defense / Mitigation:

Sanitize filenames in web applications.

Block dangerous characters (; | & $ * ?) and validate input.



---

🔹 Level 2 → 3

Challenge: File has spaces in the filename.

Solution Command:

cat "spaces in this filename"
# OR
cat spaces\ in\ this\ filename

Step-by-Step Explanation:

Shell interprets spaces as separators; quotes or escaping preserve the literal filename.


Real-World Scenario:

> Hackers hide malicious files using spaces or unusual characters (shell .php, config .env) to bypass filters.
Example: Malware often uses spaces, unicode, or invisible characters to avoid detection (SANS Whitepaper).



Teaching Points:

Quoting filenames is essential when scripting or enumerating files.

Use ls -b to reveal hidden or unprintable characters.


Defense / Mitigation:

Normalize filenames before saving.

Reject unexpected characters in uploads.

Whitelist allowed file extensions.



---

🔹 Level 3 → 4

Challenge: Find the password in a hidden file.

Solution Command:

ls -a
cat inhere/.hidden

Step-by-Step Explanation:

ls -a shows all files, including hidden files (those starting with .).

Hidden files often contain credentials, keys, or configuration data.


Real-World Scenario:

> Exposed .git, .env, or .ssh/ files often lead to serious breaches.
Example: Uber’s 2016 breach involved a publicly exposed GitHub repository containing AWS keys (Reuters).



Teaching Points:

Always check for hidden files during post-exploitation or system enumeration.

Useful commands: find . -name ".*" and grep -r "password" . for deeper checks.


Defense / Mitigation:

Block hidden files from public access.

Store secrets in secure vaults (AWS Secrets Manager, HashiCorp Vault).

Properly configure .gitignore and server permissions.



