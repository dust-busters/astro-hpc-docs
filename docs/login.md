# Login

## Register on the INDACO cluster

The astro machines sit behind the INDACO login nodes, so you need an INDACO account first. Register at [indaco.unimi.it](https://www.indaco.unimi.it/autenticazione/firstAccess.html) with your UNIMI credentials. More detail on the procedure (in Italian) is at [Registrazione UNIMI](https://www.indaco.unimi.it/index.php/registrazione-unimi/).

## Log in

Log into INDACO with your UNIMI password, then hop to an astro node (it asks for the password again):

```bash
ssh name.surname@loginng.indaco.unimi.it
ssh astro01
```

!!! note "Students"
    With a `@studenti.unimi.it` account your username is `name.surname.stud`.

## Login from outside Italy

The university firewall blocks INDACO from many foreign countries. From abroad, connect through the Department VPN first. Configuration files and instructions are on the [Department computing page](https://calcolo.mi.infn.it/?page_id=2902). Credentials are your usual UNIMI ones, with the username written without `@unimi.it`.

Recommended clients:

- **macOS**: [Tunnelblick](https://tunnelblick.net/downloads.html)
- **Linux**: GNOME Network Manager (already there if you run GNOME) or OpenVPN
- **Windows**: [OpenVPN Connect](https://openvpn.net/client/client-connect-vpn-for-windows/)

## Passwordless login

### 1. Create an SSH key

Skip this if you already have one. On **your laptop**, run `ssh-keygen` and follow the prompts. If you set a passphrase you'll be asked for it each time the key is used; press `Enter` to leave it empty. Keys go in `~/.ssh/` by default.

### 2. Copy the public key to INDACO

```bash
ssh-copy-id <username>@loginng.indaco.unimi.it
```

### 3. Jump straight to the astro nodes

Add this to `~/.ssh/config` on your laptop, replacing `<username>` with `name.surname`. Check the key path matches yours (`id_ed25519` is the usual default).

```
Host astro??
  HostName %h
  User <username>
  IdentityFile ~/.ssh/id_ed25519
  Port 22
  ProxyJump <username>@loginng.indaco.unimi.it
```

After this, `ssh astro03` from your laptop takes you straight to the node.

## Remote desktop through VNC

### First-time setup

1. SSH into INDACO, then into an astro node. This example uses `astro02`.
2. Run `vncserver` once so it creates the directories it needs.
3. Append the following to `~/.vnc/xstartup`:

    ```bash
    # Start Fluxbox
    if [ -x /usr/bin/fluxbox ]; then
        exec /usr/bin/fluxbox
    else
        echo "Fluxbox not installed or not found in /usr/bin"
        exit 1
    fi
    ```

4. Optionally `cd` into your own directory.
5. Start the server, adjusting the geometry to your screen resolution:

    ```bash
    vncserver -geometry 3456x2234
    ```

    It asks you to set a password and prints a line such as
    `New 'astro02.indaco.unimi.it:1 (<username>)' desktop is astro02.indaco.unimi.it:1`.
    Note the display number (`:1`); it increases if you open more sessions on the same node.

6. Back on your laptop, install a VNC client. Some options are listed on the [Leiden helpdesk VNC page](https://helpdesk.strw.leidenuniv.nl/wiki/doku.php?id=vnc). This guide uses RealVNC (it needs an account).
7. In RealVNC add a new connection with `VNC Server: 127.0.0.1:1` (use `:2` etc. to match the display number from step 5) and a name that tells you what the session is for.

### Every time you connect

1. Open a tunnel from your laptop (it may also work without this):

    ```bash
    ssh -NfL 5901:astroXX:5901 <username>@loginng.indaco.unimi.it
    ```

    For display `:2` use port `5902`, and so on.

2. Open your session in RealVNC.
3. Enter the password you use for the INDACO cluster.
