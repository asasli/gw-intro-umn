# LIGO Data Grid (LDG) / IGWN

A detailed user guide is available at:
- [LIGO Computing Guide](https://computing.docs.ligo.org/guide/)
- [LIGO Data Grid](https://ldg.ligo.org)

## Account Setup

- Request an account at: [https://ldg.ligo.org/](https://ldg.ligo.org/)
- Be notified by LDAS when your account is provisioned (e.g., at LIGO-Caltech).

### Account Details:
- **Username:** `albert.einstein`
- **Home Directory:** `/home/albert.einstein`
- **Global Scratch Directory:** `/scratch/albert.einstein` (shared filesystem between all hosts)
- **Local Scratch Directory:** `/local/albert.einstein` (separate filesystem for each host)

## Login Hosts for Interactive Use

| Host         | Purpose                      | RAM  | CPU                   | Cores | GPUs |
|--------------|------------------------------|------|-----------------------|-------|------|
| ldas-grid    | Production submit           |  64G | AMD EPYC 7402         |  16   | -    |
| ldas-pcdev1  | Large mem/post-processing   |   1T | AMD EPYC 7H12         | 128   | -    |
| ldas-pcdev2  | GPU mixed                   | 256G | AMD EPYC 7502P        |  32   |  4   |
| ldas-pcdev3  | GPU mixed                   | 128G | Intel E5-2670         |  16   |  3   |
| ldas-pcdev4  | LSCSOFT update testing      | 128G | Intel E5-2640 v3      |  16   | -    |
| ldas-pcdev5  | Post-processing             | 512G | Intel E5-2698 v4      |  40   | -    |
| ldas-pcdev6  | Large mem/Post-processing   | 1.5T | Intel Gold 6154       |  72   | -    |
| ldas-pcdev8  | Rocky Linux 8.5 TITAN V GPU |  96G | Intel Gold 5115       |  10   |  1   |
| ldas-pcdev10 | Skylake Benchmarking        |  64G | Intel E3-1240 v5      |   4   | -    |
| ldas-pcdev11 | GPU mixed                   | 128G | Intel E5-2630 v4      |  20   |  4   |
| ldas-pcdev12 | GPU 4 x A100-SXM4-80GB      | 512G | AMD EPYC 7763         | 128   |  4   |
| ldas-pcdev13 | GPU mixed                   | 128G | Intel E5-2650 v4      |  24   |  4   |
| ldas-pcdev14 | Large mem benchmarking      | 256G | AMD Opteron 6376      |  16   | -    |
| ldas-osg     | IGWN OSG submit machine     | 196G | Intel Gold 6136       |  24   | -    |
| ldas-osg2    | IGWN OSG submit machine     |  32G | AMD EPYC 7402         |   4   | VM   |

### Web Server (No Logins)
- **Host:** `ldas-jobs.ligo.caltech.edu`
- **Pages Directory:** `~/public_html` on login machines.
- **CGI Support:** Supported with `.cgi` extension.
- **URL:** [https://ldas-jobs.ligo.caltech.edu/~argyro.sasli](https://ldas-jobs.ligo.caltech.edu/~argyro.sasli)

## Computing Inquiries
For assistance, contact: `ldas_admin_cit@ligo.caltech.edu`

## Getting Started Documentation
- [LDG Tools and Utilities](https://wiki.ligo.org/Computing/LDG/GettingStarted)
- [Grid Credentials](https://wiki.ligo.org/Computing/LDG/GridCredentials)

### DASWG Resources
- **Mailing List:** [Subscribe to DASWG](http://www.lsc-group.phys.uwm.edu/daswg/participate/mailinglist.html)

### CIT Clusters
- [CIT Computing Guide](https://computing.docs.ligo.org/guide/computing-centres/cit/)

## SSH Login Authentication Methods

### 1. Kerberos Credential
To access the LIGO Data Grid, you need Kerberos and X.509 credentials:

1. Install Kerberos (available on OS X or from [MIT Kerberos](https://web.mit.edu/kerberos/) for other OS).
2. Run the following command:
   ```bash
   kinit firstname.lastname@LIGO.ORG
   ```
   Replace `firstname.lastname` with your LIGO.org username. Enter your LIGO.org passphrase.
3. Login example:
   ```bash
   ssh -K albert.einstein@ldas-grid.ligo.caltech.edu
   ```

More details: [Kerberos SSH Login](https://wiki.ligo.org/Computing/LDG/KerberosSSHLogin).

#### Simplify Login with Config:
**Option 1:**
Edit `~/.ssh/config`:
```bash
Host ldas-grid.ligo.caltech.edu
User albert.einstein
```

**Option 2:**
Add these lines to `~/.ssh/config`:
```bash
Host ldas-grid.ligo.caltech.edu
User albert.einstein
GSSAPIDelegateCredentials yes
GSSAPIAuthentication yes
```

### 2. SSH Public Key
1. Manage your SSH keys via [LDG Account Management](https://grouper.ligo.org/ldg/manage_ssh).
2. Add your local public SSH key via [My LIGO Account](https://my.ligo.org/).
3. Verify your default username and server access.

### 3. LIGO.org Password
Follow [LDG Client Software Installation Guide](https://www.lsc-group.phys.uwm.edu/lscdatagrid/doc/installclient.html).

## Generating X.509 Credentials
Install the [LDG Client Software](https://computing.docs.ligo.org/guide/software/ldg-client/):
- Generates X.509 certificates.
- Installs `gsissh` (replaces `ssh`) and `gsiscp` (replaces `scp`).

To generate a proxy:
```bash
ligo-proxy-init firstname.lastname
```
Example:
```bash
ligo-proxy-init albert.einstein
```
Enter your LIGO password. The proxy is valid for ~10-12 days and must be regenerated after expiration.

## Accessing LDG Clusters
Find an updated list of clusters: [LDG WebHome](https://wiki.ligo.org/Computing/LDG/WebHome)

Login example:
```bash
gsissh albert.einstein@ldas-grid.ligo.caltech.edu
```

## LIGO SSH Login Portal
You can also access LDG clusters using the SSH Login Portal (SLP). No special software or certificates are required. Example:
```bash
ssh albert.einstein@ssh.ligo.org
```
Enter your LIGO password.

## Copying Files
### From Local PC to LDG:
```bash
scp ~/where/the/file/lives/in albert.einstein@ldas-grid.ligo.caltech.edu:~/where/to/copy/the/file
```
Example:
```bash
scp ~/GW150914/H-H1_GWOSC_16KHZ_R1-1126259447-32.gwf albert.einstein@ldas-grid.ligo.caltech.edu:~/Basic_Tests/
