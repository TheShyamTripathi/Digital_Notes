To edit the commit message that has already been posted to GitHub, you need to amend the commit locally and then force-push the change. Here's how you can do it:

### If it's the most recent commit:
1. **Amend the commit message locally:**
   - Run the following command in your terminal:
     ```
     git commit --amend
     ```
   - This will open your default text editor, allowing you to modify the commit message. After editing, save and close the editor.

2. **Force-push the amended commit:**
   - To update the commit message on GitHub, you need to force-push the changes:
     ```
     git push --force
     ```
   - This will overwrite the commit on the remote repository with your amended message.

### If you need to change an older commit message:
1. **Interactive rebase:**
   - Start an interactive rebase:
     ```
     git rebase -i HEAD~n
     ```
   - Replace `n` with the number of commits you want to go back (e.g., if you want to edit the commit message from 3 commits ago, replace `n` with 3).

2. **Edit the commit message:**
   - In the editor that opens, find the commit message you want to change. Replace the word `pick` with `reword` next to the commit you want to modify. Save and close the editor.
   - Another editor window will open for you to change the commit message. Make your changes, then save and close.

3. **Complete the rebase:**
   - After editing the commit message(s), you'll need to complete the rebase process. If there are no conflicts, Git will automatically finish the rebase.

4. **Force-push the updated commit:**
   - Finally, force-push the changes to GitHub:
     ```
     git push --force
     ```

### Important Notes:
- **Force-pushing can overwrite history on the remote repository.** If others have pulled from this branch, it can cause issues for them. Make sure you're aware of the potential impact.
- Consider informing your collaborators if you are force-pushing changes.

Let me know if you need further assistance with this!
