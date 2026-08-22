# Edge Toolkit

```text
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣠⠄⠀⠀⠀⢀⣴
⠀⠀⠀⠀⠀⠀⠀⢀⣠⣤⣤⣙⠋⠀⠀⢀⣴⣿⡇⠀⠀⠀⠀⠀⡰
⠀⠀⢀⣠⣤⣶⢿⣏⢉⠉⠒⠂⠀⠠⣀⠛⠿⡼⠀⠀⠀⠀⢀⡔⠁
⣰⣇⣸⣯⣷⣾⣿⣿⣾⠇⢀⣀⣠⣮⣮⢧⢰⠀⠀⠀⢀⣴⡟⠀⠀⡀
⢻⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⡿⣱⠏⠀⣀⣴⣾⣿⣷⣤⣾⠁
⣇⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⡱⢃⣠⣾⣿⣿⣿⢿⣿⣿⢃⡄
⣭⡛⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣾⣾⣿⣿⣿⣿⣿⣿⣼⣿⣧⡟
⣿⣿⣷⣮⣙⠿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⠿⠿⣿⢇⣿⠟⠄⣼
⢿⣿⣿⣿⣿⣷⣮⡝⣿⣿⢟⣉⣙⡫⠭⠭⠛⠛⣛⣿⣶⡿⣩⡾⣸⣿
⠘⣿⣿⣿⣿⣿⠟⣵⡿⢡⣿⣿⣿⣿⢸⢀⣠⣾⣿⠿⠋⣼⣿⢣⣿⣿
⠀⣿⣿⣿⡿⢃⠻⣿⣧⣂⠭⠭⠭⠕⣢⣾⡿⡋⣴⣾⢸⡟⠟⣼⣿⣿
⠀⢻⡿⢟⣴⣿⣿⣮⡙⠿⣿⣿⣿⡿⢛⣵⣾⣇⢿⡿⡜⢧⠀⣿⣿⠿
⠀⠘⣱⣾⣿⣿⣿⣿⣿⣷⣦⣭⣵⣾⣿⠿⠿⣛⡼⣼⡿⡷⣭⡭⣵⣿
```

For my Next.js applications, I typically use PostgreSQL, Nginx, Cloudflare Origin Certificates, Node.js, and PM2. Setting up and configuring all of these components manually is tedious and error-prone. That’s why I created this toolkit to automate the installation and configuration of the core infrastructure required to deploy and run Next.js applications.

Simply clone the repository, run the `edge` command, and the environment is ready to use. The toolkit also includes a customized MOTD and a dedicated command to access the management menu for the installed tools.

Feel free to extend the toolkit, add new features, or contribute improvements. The goal is to evolve it into a more powerful and flexible server provisioning toolkit over time, supporting additional tools, services, and deployment scenarios. Contributions and new ideas are welcome. The more capabilities we add, the more useful the toolkit becomes for quickly provisioning production-ready environments.

## Installation

Clone the repository and navigate to the project directory:

```bash
git clone <repository-url>
cd edgevps
```

The repository contains two main files:

* `edge` — the source code for the `edge` CLI, installed as `/usr/local/bin/edge`.
* `motd` — the custom Message of the Day displayed when users log in via SSH.

### 1. Install the `edge` CLI

Install the `edge` command system-wide and make it executable:

```bash
sudo cp edge /usr/local/bin/edge
sudo chmod +x /usr/local/bin/edge
```

You can verify the installation with:

```bash
edge --help
```

### 2. Configure the MOTD

On Debian-based systems such as Ubuntu, the Message of the Day can be generated dynamically by scripts located in `/etc/update-motd.d/`. These scripts may add or replace content displayed during SSH login.

To ensure that the Edge Toolkit MOTD is displayed consistently, disable the default MOTD scripts:

```bash
sudo chmod -x /etc/update-motd.d/*
```

Then install the custom MOTD:

```bash
sudo cp motd /etc/motd
```

Verify the installed MOTD:

```bash
cat /etc/motd
```

You can also manually execute the MOTD scripts to test the system's dynamic MOTD configuration:

```bash
sudo run-parts /etc/update-motd.d/
```

Finally, open a new SSH session to verify that the custom MOTD is displayed correctly during login.

> **Note:** Disabling the scripts does not remove them from the system. It only prevents them from being executed. They can be re-enabled at any time with `chmod +x`.

### 3. Launch the Toolkit

Once the `edge` CLI is installed, launch the management interface:

```bash
sudo edge
```

The `edge` command provides access to the toolkit's management menu and available infrastructure operations.

### 4. Install the Required Stack

From the toolkit, use the installation command to provision the required infrastructure:

```bash
sudo edge --install
```

This installs and configures the core components required for a typical Next.js production environment, including:

* Node.js
* PM2
* Nginx
* PostgreSQL
* Cloudflare Origin Certificates

Once the installation process completes, the server is ready for Next.js application deployment.

### Manual Installation Flow

For a quick setup, the complete installation flow can be performed with:

```bash
git clone <repository-url>
cd edgevps

sudo cp edge /usr/local/bin/edge
sudo chmod +x /usr/local/bin/edge

sudo chmod -x /etc/update-motd.d/*
sudo cp motd /etc/motd

sudo edge --install
```

After installation, use:

```bash
sudo edge
```

to access the Edge Toolkit management interface.
