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

## git workflow solo dev

- Best Practices for Git (Solo Developer on Two Laptops)
- Always pull latest main before creating a feature branch.
- Small commits: Keep your commits focused (1 commit = 1 logical change ideally).
- Commit messages: Write clear messages (e.g., feat: add chapter 3 initial logic).
- Rebase often your feature branch on main (especially if working over multiple days).
- Squash commits when merging feature branches into main (optional but recommended if you have many small messy commits).
- Delete merged feature branches (you’re already doing it!).

### Safe Commands to Remember  (solo dev)
```sh
# 1. Create a new feature branch locally
git checkout main
git pull origin main
git checkout -b feature/chapter3

# 2. Work, commit changes
git add .
git commit -m "feat: add initial setup for chapter3"

# 3. Push your branch to remote (optional, if you want sync)
git push origin feature/chapter3

# 4. Keep rebasing on top of latest main (do it often)
git fetch origin
git rebase origin/main

# 5. Once done, squash merge into main
git checkout main
git pull origin main
git merge --squash feature/chapter3
git commit -m "feat: complete chapter 3"

# 6. Push updated main
git push origin main

# 7. Delete feature branch locally and remotely
git branch -d feature/chapter3
git push origin --delete feature/chapter3
```

## Best Git Practices for a 2–3 Person Team  

1. Everyone works off the main branch indirectly 
    - No one directly commits to main.  
    - Always create a feature branch → work → then merge back into main.  

Example feature branches:
```
feature/login-page
bugfix/navbar-crash
chore/update-readme
```
2. Push feature branches to remote  
    - You must push your feature branches (so teammates can see and collaborate if needed).
3. Keep feature branches updated with main
    - Regularly fetch and rebase your feature branch on top of the latest main. Avoid big, scary merge conflicts at the end.
4. Use Pull Requests (PRs) or Merge Requests (MRs)
    - Create a PR for every feature branch to merge into main. and Catch mistakes early, Make sure everyone knows what changes are coming.
5. Squash and Merge into main
    - This keeps the main history very clean and readable.
6. Clean up merged feature branches
    - After merging, delete the remote feature branch.

### In Short: Your Git Workflow in Small Team
```sh
# 1. Update main
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/your-feature-name

# 3. Work, then stage and commit
git add .
git commit -m "feat: add description"

# 4. Push feature branch
git push origin feature/your-feature-name

# 5. Keep updated with main
git fetch origin
git rebase origin/main

# 6. After PR merged, cleanup
git branch -d feature/your-feature-name
git push origin --delete feature/your-feature-name

# 7. Repeat for next work
git checkout main
git pull origin main
git checkout -b feature/next-feature-name
```