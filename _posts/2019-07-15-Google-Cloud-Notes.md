---
title: Google Cloud Notes
date: 2019-07-15 12:28:12 -0500
img: gcp.jpeg
categories: [Server]
tags: [gcloud]
---
### Connect to your instance
- **Compute Engine** -> **VM instances** -> SSH downside triangle -> **View gcloud command**
- Paste the command to your terminal


### Use FileZilla on Google Cloud Platform
System is MacOS. Credit to [Using FileZilla with Google Cloud Platform on OSX](https://torbjornzetterlund.com/using-filezilla-google-cloud-platform-osx/). Windows users can check [this post](https://www.onepagezen.com/google-cloud-ftp-filezilla-quick-start/).
1. Generate ssh key on your local laptop.
    - `ssh-keygen -t rsa -f ~/.ssh/wp-ssh-key -C [USERNAME]` You can find [USERNAME] on the terminal after you connect to the instance.
    - `chmod 400 ~/.ssh/wp-ssh-key` Restrict access.
    - `cat ~/.ssh/wp-ssh-key.pub` Obtain and copy the contents of public key.
2. Paste the ssh key on GCP.
    - **Compute Engine** -> **Metadata** -> **SSH Keys** -> **Edit** -> **+Add item** -> paste the public key -> **Save**
3. Use the ssh key to connect to your instance
    - `ssh -i ~/.ssh/wp-ssh-key [USERNAME]@[IP_ADDRESS]` \[IP_ADDRESS\]is the external IP of the instance.
4. Set up FileZilla
    - **Edit** -> **Settings...** -> **SFTP** -> **Add key file...** First copy `~/.ssh/wp-ssh-key` to some place then choose it.
    - Fill in the information in the interface. **Host**: `sftp://[IP_ADDRESS]`, **Username**: `[USERNAME]`.
    - **Quickconnect**
