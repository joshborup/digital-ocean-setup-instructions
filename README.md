# Digital Ocean coupons and setup instructions

<ol>
    <li>First open this <a href='https://m.do.co/c/14d81c9a2d3a'>link</a> and Sign Up to get your $10 credit.</li>
    <li>While filling your billing info, click on "Have a Promo Code?" at the bottom of the page.</li>
    <li>Enter any one of the below codes to get extra credit:</li>
</ol>

<ul>
    <li>CodeAnywhere10</li>
    <li>LOWENDBOX</li>
    <li>CODEANYWHERE</li>
    <li>DOPRODUCT15</li>
    <li>DO10</li>
    <li>ALLSSD10</li>
    <li>WP10</li>
    <li>DROPLET10</li>
    <li>BITNAMI</li>
    <li>DEPLOY10</li>
    <li>ACTIVATE10</li>
    <li>DONEWS</li>
    <li>FRANKFURT</li>
</ul>

<strong>these instructions were selectively copied from the relevant portions of digital ocean's documentations</strong>


# Initial Server Setup

## Step One -- Root Login

if you are not already connected to your server, go ahead and log in as the root user using the following command (substitute the highlighted word with your server's public IP address):

``` bash
ssh root@your_server_ip
```

## Step Two — Create a New User
Once you are logged in as root, we're prepared to add the new user account that we will use to log in from now on.

This example creates a new user called "devmountain", but you should replace it with a username that you like:

```bash
adduser devmountain
```

## Step Three — Root Privileges

Now, we have a new user account with regular account privileges. However, we may sometimes need to do administrative tasks.

To avoid having to log out of our normal user and log back in as the root account, we can set up what is known as "superuser" or root privileges for our normal account. This will allow our normal user to run commands with administrative privileges by putting the word sudo before each command.

As root, run this command to add your new user to the sudo group (substitute the highlighted word with your new user):

```bash
usermod -aG sudo sammy
```

## Step Four — Add Public Key Authentication (Recommended)

The next step in securing your server is to set up public key authentication for your new user. Setting this up will increase the security of your server by requiring a private SSH key to log in.

### Generate a Key Pair
If you do not already have an SSH key pair, which consists of a public and private key, you need to generate one. If you already have a key that you want to use, skip to the Copy the Public Key step.

To generate a new key pair, enter the following command at the terminal of your local machine (ie. your computer):

```bash
ssh-keygen
```

Assuming your local user is called "localuser", you will see output that looks like the following:

```bash
ssh-keygen output
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/localuser/.ssh/id_rsa):
Hit return to accept this file name and path (or enter a new name).
```

Next, you will be prompted for a passphrase to secure the key with. You may either enter a passphrase or leave the passphrase blank.

This generates a private key, id_rsa, and a public key, id_rsa.pub, in the .ssh directory of the localuser's home directory. Remember that the private key should not be shared with anyone who should not have access to your servers!

### Copy the Public Key

use the following command at the terminal of your local machine to print your public key (id_rsa.pub):

```bash
cat ~/.ssh/id_rsa.pub
```

This should print your public SSH key, which should look something like the following:

```bash
id_rsa.pub contents
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBGTO0tsVejssuaYR5R3Y/i73SppJAhme1dH7W2c47d4gOqB4izP0+fRLfvbz/tnXFz4iOP/H6eCV05hqUhF+KYRxt9Y8tVMrpDZR2l75o6+xSbUOMu6xN+uVF0T9XzKcxmzTmnV7Na5up3QM3DoSRYX/EP3utr2+zAqpJIfKPLdA74w7g56oYWI9blpnpzxkEd3edVJOivUkpZ4JoenWManvIaSdMTJXMy3MtlQhva+j9CgguyVbUkdzK9KKEuah+pFZvaugtebsU+bllPTB0nlXGIJk98Ie9ZtxuY3nCKneB+KjKiXrAvXUPCI9mWkYS/1rggpFmu3HbXBnWSUdf localuser@machine.local
```