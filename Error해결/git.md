# git

## gitignore가 작동하지 않을때

```bash
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
```