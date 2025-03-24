# Implementing LLM and AI related things from scratch


## local git setup
1. Navigate to Your Project Directory
```sh
cd /path/to/your/project
```
2. Set Up a Local Git User
```sh
git config user.name "Your New Name"
git config user.email "your-new-email@example.com"
```
Verify the Configuration
```sh
git config --get user.name
git config --get user.email
```

3. Use SSH Instead of HTTPS (Optional, Recommended for Security)

(a) Generate a New SSH Key (Only if You Don’t Have One)
Run this command to create a new SSH key:

```sh
ssh-keygen -t rsa -b 4096 -C "your-new-email@example.com"
```
- When prompted, save it as a new file (e.g., ~/.ssh/id_rsa_personal) so it doesn’t overwrite office SSH keys.
- Skip setting a passphrase if you don’t want to enter it every time.

(b) Add the New SSH Key to SSH Agent
Start the SSH agent:
```sh
eval "$(ssh-agent -s)"
```
Then add your new key:
```sh
ssh-add ~/.ssh/id_rsa_personal
```
(c) Add the Key to Your GitHub Account
1. Copy the key to the clipboard:
```sh
cat ~/.ssh/id_rsa_personal.pub
```
2. Go to GitHub → Settings → SSH and GPG keys.
3. Click New SSH Key, paste the key, and save.

(d) Update the Git Remote to Use SSH
Switch the repo from HTTPS to SSH:

```sh
git remote set-url origin git@github.com:your-username/your-repo.git
```
