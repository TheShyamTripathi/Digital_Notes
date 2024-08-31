To ensure that newly initialized Git repositories in your system have `main` as the default branch instead of `master`, you can configure Git's default branch name globally. Here's how to do it:

### Set `main` as the Default Branch for New Repositories

1. Open your terminal or command prompt.

2. Run the following command to configure Git to use `main` as the default branch for new repositories:

   ```bash
   git config --global init.defaultBranch main
   ```

### Verify the Configuration

You can verify that the setting has been applied by checking your Git configuration:

```bash
git config --global --get init.defaultBranch
```

This should return `main`, indicating that any new repositories you initialize will use `main` as the default branch.

### Testing It

Now, when you create a new Git repository, it should automatically use `main` as the default branch:

```bash
git init new-repo
cd new-repo
git branch
```

You should see `* main` as the active branch.

This configuration will only affect new repositories that you initialize. For existing repositories, you would need to rename the branch manually, as described earlier.
