# First Steps

Create your Ubuntu DigitalOcean droplet through their portal. Ensure you enable SSH authentication and select your key.

## SSH in to droplet

First you will need to SSH in as the root user.

```bash
ssh root@[ip]
```

## Set root password

```bash
passwd
```

This will allow you to set a password for your root user. Be sure to use a secure password to protect your server.

## Create a non-root user

In these next steps, replace `nhcarrigan` with the username you would like.

```bash
adduser nhcarrigan
```

This will prompt you to set a password (this should be different from your root password), and provide basic user information (personally, I set the name and leave everything else blank).

```txt
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for nhcarrigan
Enter the new value, or press ENTER for the default
        Full Name []: Nicholas Carrigan
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
Is the information correct? [Y/n] y
```

## Grant new user admin

To give your new user the ability to run things with `sudo`, use this:

```bash
usermod -aG sudo nhcarrigan
```

## Copy SSH Keys

If you set up SSH authentication for your droplet (which you should), your keys only work for the root user. Add them to your new user with:

```bash
rsync --archive --chown=nhcarrigan:nhcarrigan ~/.ssh /home/nhcarrigan
```

> [!WARNING]
> SSH permissions are tricky. It is imperative that you do *not* edit the permissions of your /home/nhcarrigan directory OR the .ssh directory within.

After completing these steps, close your SSH connection and attempt to SSH in as your new user instead of `root`. If you followed these instructions correctly, you'll now be logged in as your new user.

## Set Timezone

Make sure you set your server timezone appropriately. I usually set it to my local timezone.

```bash
sudo timedatectl set-timezone <your_timezone>
```
