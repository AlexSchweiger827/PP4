# PP4

## Goal

In this exercise you will:

* Use SSH to connect to remote servers from WSL, macOS, or Linux shells, understanding the handshake and authentication process.
* Generate an Ed25519 SSH key pair and explain the concept of digital signatures.
* Configure your local SSH client via the `~/.ssh/config` file for streamlined access.
* Securely copy files between local and remote hosts using `scp`, including local-to-remote, remote-to-local, and remote-to-remote transfers.
* Automate startup tasks on the remote server by writing a shell script that runs at login and explaining the role of `~/.bashrc` vs. `~/.profile`.

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and record exactly where you paused.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=SSH%3A](https://github.com/orgs/STEMgraph/repositories?q=SSH%3A)
* Consult the SSH and SCP man-pages for detailed options and explanations:

  * `man ssh`
  * `man scp`

---

## Tasks

### Task 1: SSH Login

**Objective:** Establish an SSH connection and observe each stage of the process.

1. From your local shell (WSL, macOS Terminal, or Linux), log into the `vorlesungsserver` (or any other remote machine of your choice, e.g. your own raspberry pi):

   ```bash
   ssh youruser@remotehost
   ```
2. Carefully observe and note each step:

   * **TCP connection** to port 22 on `remotehost`.
   * **SSH protocol handshake**: key exchange and algorithm negotiation.
   * **Authentication**: public-key or password exchange.
   * **Shell allocation**: your remote session starts.
3. After login, exit the session with `exit`.

**Provide:**

```bash
# 1) The exact ssh command you ran

command:
ubuntu@ubuntu:~$ ssh ubuntu@172.31.1.161



command:
ubuntu@DESKTOP-6IB5N3D:~$ exit
g
output:
logout
Connection to 172.31.1.161 closed.

# 2) A detailed, step-by-step explanation of what happened at each stage

1.TCP connection
First I wrote the command "ssh ubuntu@172.31.1.161".
With this command I made an ssh connection to the host on port 22

Output:
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug1: Connecting to 172.31.1.161 [172.31.1.161] port 22.
debug1: Connection established.


2.SSH prtocol handshake
The client and the server exchange their supported SSH protocol versions to ensure that the connection is compatible.

Output:
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: sntrup761x25519-sha512@openssh.com
debug1: kex: host key algorithm: ssh-ed25519
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: SSH2_MSG_KEX_ECDH_REPLY received
debug1: Server host key: ssh-ed25519 SHA256:HfPJ+11rq5bhNzyXhIgM7Kkni6zF+8MvIaqlNSXXyvE
debug1: load_hostkeys: fopen /home/ubuntu/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: Host '172.31.1.161' is known and matches the ED25519 host key.
debug1: Found key in /home/ubuntu/.ssh/known_hosts:1
debug1: ssh_packet_send2_wrapped: resetting send seqnr 3
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: Sending SSH2_MSG_EXT_INFO
debug1: expecting SSH2_MSG_NEWKEYS
debug1: ssh_packet_read_poll2: resetting read seqnr 3
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey in after 134217728 blocks
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_ext_info_client_parse: server-sig-algs=<ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,rsa-sha2-512,rsa-sha2-256>
debug1: kex_ext_info_check_ver: publickey-hostbound@openssh.com=<0>
debug1: kex_ext_info_check_ver: ping@openssh.com=<0>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_ext_info_client_parse: server-sig-algs=<ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,rsa-sha2-512,rsa-sha2-256>
debug1: Authentications that can continue: publickey,password

3.Authentication
I had to authenticate the client by typing the password that the server created for the client.
An other method would be a public key authentication. In that case the server would send a public key to the client.
The client can then authenticate himself through the public key and without a password.

Output:

debug1: Next authentication method: publickey
debug1: get_agent_identities: bound agent to hostkey
debug1: get_agent_identities: ssh_fetch_identitylist: agent contains no identities
debug1: Will attempt key: /home/ubuntu/.ssh/id_rsa
debug1: Will attempt key: /home/ubuntu/.ssh/id_ecdsa
debug1: Will attempt key: /home/ubuntu/.ssh/id_ecdsa_sk
debug1: Will attempt key: /home/ubuntu/.ssh/id_ed25519
debug1: Will attempt key: /home/ubuntu/.ssh/id_ed25519_sk
debug1: Will attempt key: /home/ubuntu/.ssh/id_xmss
debug1: Trying private key: /home/ubuntu/.ssh/id_rsa
debug1: Trying private key: /home/ubuntu/.ssh/id_ecdsa
debug1: Trying private key: /home/ubuntu/.ssh/id_ecdsa_sk
debug1: Trying private key: /home/ubuntu/.ssh/id_ed25519
debug1: Trying private key: /home/ubuntu/.ssh/id_ed25519_sk
debug1: Trying private key: /home/ubuntu/.ssh/id_xmss
debug1: Next authentication method: password
ubuntu@172.31.1.161's password:
Authenticated to 172.31.1.161 ([172.31.1.161]:22) using "password".
debug1: channel 0: new session [client-session] (inactive timeout: 0)
debug1: Requesting no-more-sessions@openssh.com
debug1: Entering interactive session.

4. Shell allocation
After the Authentication was successful, the server made a shell for interactions between client and server.
In my case I was logged in to the remote machine. My prompt changed from "ubuntu@ubuntu" to "ubuntu@DESKTOB-6IB5N3D".

Output:
debug1: pledge: filesystem
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug1: client_input_hostkeys: searching /home/ubuntu/.ssh/known_hosts for 172.31.1.161 / (none)
debug1: client_input_hostkeys: searching /home/ubuntu/.ssh/known_hosts2 for 172.31.1.161 / (none)
debug1: client_input_hostkeys: hostkeys file /home/ubuntu/.ssh/known_hosts2 does not exist
debug1: Sending environment.
debug1: channel 0: setting env LANG = "C.UTF-8"
Learned new hostkey: RSA SHA256:6IqZJiDt91bbEf9YXC2p17RS7RL1i7rRMvoVXiGe46M
Learned new hostkey: ECDSA SHA256:0wUEgjOaLqoqlPZxf8KnAm4EEN5E8LytY3wgxfzHlFo
Adding new key for 172.31.1.161 to /home/ubuntu/.ssh/known_hosts: ssh-rsa SHA256:6IqZJiDt91bbEf9YXC2p17RS7RL1i7rRMvoVXiGe46M
Adding new key for 172.31.1.161 to /home/ubuntu/.ssh/known_hosts: ecdsa-sha2-nistp256 SHA256:0wUEgjOaLqoqlPZxf8KnAm4EEN5E8LytY3wgxfzHlFo
debug1: update_known_hosts: known hosts file /home/ubuntu/.ssh/known_hosts2 does not exist
debug1: pledge: fork

by writing the command "exit" you will close the connection with the host.
```


---

### Task 2: Ed25519 Key Pair

**Objective:** Create a secure key pair and explain how digital signatures verify identity.

1. Generate an Ed25519 SSH key pair:

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   * Accept the default file location (`~/.ssh/id_ed25519`). Or provide the `-f <filepath>` option additionally.
   * Enter a passphrase when prompted (optional).
2. Locate and inspect your `id_ed25519` (private key) and `id_ed25519.pub` (public key).
3. Install your key on the remote machine (e.g. `vorlesungsserver`.
4. Explain in writing:

   * How the **private key** is used to sign challenges.
   * How the **public key** on the server verifies signatures without revealing the private key.
   * Why Ed25519 is preferred (performance, security).

**Provide:**

```bash
# 1) The ssh-keygen command you ran

ssh-keygen -t ed25519 -C "Alexander.schweiger@stud.thga.de"

# 2) The file paths of the generated keys

/home/lex-alex/.ssh/id_ed25519

/home/lex-alex/.ssh/id_ed25519.pub

# 3) Your written explanation (3–5 sentences) of the signature process



The private key encrypt the message. 

The public key decrypts the signature that was made by the private key. It compares the hash with its own computed hash and verifys the authencity of the signature.

Ed25519 is preferred because, it is fast in making signatures and in verifying the signatures. It also has a high safety standard. 
```

---

### Task 3: SSH Config File

**Objective:** Simplify SSH commands via `~/.ssh/config`.

1. Open (or create) `~/.ssh/config` in `vim`.
2. Add entries for your hosts, for example:

   ```text
   Host my-remote
       HostName remote.example.com
       User youruser
       IdentityFile ~/.ssh/id_ed25519

   Host backup-server
       HostName backup.example.com
       User backupuser
       Port 2222
       IdentityFile ~/.ssh/id_ed25519_backup
   ```
3. Save and close the file, then test:

   ```bash
   ssh my-remote
   ssh backup-server
   ```
4. Explain:

   * How SSH reads `~/.ssh/config` and matches hosts.
   * The difference between `HostName` and `Host`.
   * How aliases prevent long commands.

**Provide:**

```text
# 1) The full contents of your ~/.ssh/config

Host my-remote
       HostName 172.31.1.161
       User ubuntu
       IdentityFile ~/.ssh/id_ed25519


Host backup-server
               HostName 172.31.1.161
               User ubuntu
               Port 2222
               IdentityFile ~/.ssh/id_ed25519_backup

Host is the alias for the server. The client also can login through this name.

The HostName is the real name or rather the real address of the server.

By changing the server adress to an alias the command for an ssh connection is very simple und terminates writing mistakes.

# 2) A short explanation (3–4 sentences) of how the config simplifies connections


By creating a remote server in this way, you do not need to write a long command like "ssh ubuntu@172.31.1.161".
You can join the remote server by writing for example "ssh my-remote".
It safes time and you do not need to remember the Hostnames like "172.31.1.161".

```

---

### Task 4: SCP File Transfers

**Objective:** Practice copying files securely using `scp`.

1. **Local → Remote**:

   ```bash
   scp test.txt ubuntu@172.31.1.161:~/home
   ```
2. **Remote → Local**:

   ```bash
   scp ubuntu@172.31.1.161:~/test_remote.txt ./home
   ```
3. **Remote → Remote** (between two directories on the same remote host):

   ```bash
   scp -r youruser@remotehost:/path/dir1 youruser@remotehost:/path/dir2
   ```
4. For each command:

   * Verify file timestamps and sizes after transfer, using `ls -la`
   * Note any flags you used (e.g., `-r`, `-P` for port).
5. Explain:

   * How `scp` initiates an SSH session for each transfer.
   * The role of encryption in protecting data in transit.

**Provide:**

```bash
# 1) Each scp command you ran

1. **Local → Remote**:

   ```bash
   scp test.txt ubuntu@172.31.1.161:~/home
   ```

2. **Remote → Local**:

   ```bash
   scp ubuntu@172.31.1.161:~/test_remote.txt ./home
   ```
   
# 2) Any flags or options used
# 3) A brief explanation (2–3 sentences) of scp’s mechanism

SCP (Secure Copy Protocol) is a secure file transport protocol between hosts based on the Secure Shell (SSH). It ensures that only authorized users can access and transfer. The SSH encryption protects the data during transit to prevent that unauthorized users can access and temper these files.
```

---

### Task 5: Login Shell Script & Profile Explanation

**Objective:** Automate commands at login and understand shell initialization files.

1. On the **remote** server, create a script `~/login_tasks.sh` containing at least three commands you find useful (e.g., `echo "Welcome $(whoami)"`, `uptime`, `ls ~/projects`). You may either use `vim` or try the following to create a file from your commandline directely:

   ```bash
   cat << 'EOF' > ~/login_tasks.sh
   #!/usr/bin/env bash
   echo "Welcome $(whoami)! Today is $(date)."
   uptime
   ls ~/projects
   EOF
   chmod +x ~/login_tasks.sh
   ```

> The files content should be something akin to:
> ```bash
> #!/usr/bin/env bash
> echo "Welcome $(whoami)! Today is $(date)."
> uptime
> ls ~/projects
> ```

2. Append to your `~/.bashrc` (or `~/.profile` if using a login shell) a line to source this script on each new session:

   ```bash
   echo "source ~/login_tasks.sh" >> ~/.bashrc
   ```
3. Log out and log back in to trigger the script.
4. Explain:

   * The difference between `~/.bashrc` and `~/.profile` (interactive vs. login shells).
   * Why and when each file is read.
   * How sourcing differs from executing.

**Provide:**

```bash
# 1) The contents of login_tasks.sh
# 2) The lines you added to ~/.bashrc or ~/.profile
# 3) Your explanation (3–5 sentences) of shell init files and sourcing vs. executing
```

---

**Remember:** Stop working after **90 minutes** and record where you stopped.

I did task 1-3 and started with task 4. 
