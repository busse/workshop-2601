Deploy the site: commit all changes, push, and rebuild GitHub Pages.

Steps:
1. Run `git status` and `git diff` to see what changed.
2. If there are no changes (no modified, added, or untracked files), say "Nothing to deploy — working tree is clean." and stop.
3. Stage all changed and untracked files with `git add -A`.
4. Write a conventional commit message (feat:/fix:/docs:/style:/refactor: etc.) based on the diff. Use imperative mood. Include the co-author trailer.
5. Commit the changes.
6. Push to origin.
7. Trigger the GitHub Actions workflow with: `gh workflow run "Deploy Jekyll site to Pages" --ref master`
8. Confirm the workflow was triggered by running `gh run list --limit 1`.
9. Report the result: commit hash, push status, and workflow run ID.
