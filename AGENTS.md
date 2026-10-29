# 代理開發約定

這個 repository 是個人 fork [`asdf3601a/not-shift`](https://github.com/asdf3601a/not-shift)。上游是 [`JasonHsuFet/Working_Shift`](https://github.com/JasonHsuFet/Working_Shift)，預設分支是 `main`。

## 每次開發之前

先讓 `origin/main` 對齊 `upstream/main`，再從更新後的 `origin/main` 開新分支。功能開發不要提交在 `main` 上。更新 `main` 只做這次同步。

1. 確認 `upstream` remote 存在。只對它 fetch，不要 push：

   ```bash
   git remote get-url upstream >/dev/null 2>&1 || git remote add upstream https://github.com/JasonHsuFet/Working_Shift.git
   git fetch upstream --prune
   git fetch origin --prune
   ```

2. 比較 `origin/main` 與 `upstream/main`。用 `git log origin/main..upstream/main` 列出上游多出來的提交，並用 `git diff --stat origin/main...upstream/main` 看影響的檔案。也檢查 `upstream/main..origin/main`，指出 fork 自己多出來的提交。

3. 在改程式之前，先給使用者一份繁體中文摘要。沒有新提交也要明講，並寫出兩邊共同的提交。摘要包含提交、時間（Asia/Taipei）與受影響的路徑，不要只寫「已同步」。

4. 把上游更新寫進 `origin/main`，再從它開分支：

   ```bash
   git checkout main
   git merge --ff-only upstream/main
   git push origin main
   git checkout -b <新分支> origin/main
   ```

   - `upstream/main` 可以快轉時，用上面的 `--ff-only`。不要 force-push `main`，也不要 `reset --hard`。
   - 兩邊歷史已分歧、無法快轉時，在 `main` 上 `git merge upstream/main` 產生合併提交後再 `git push origin main`。保留 fork 自己的提交。
   - 上游沒有新提交時，不要為了同步而做空提交。直接從當時的 `origin/main` 開新分支。
   - Cloud Agent 的分支名稱遵循該次工作要求的格式。
   - 對上游的 pull request 只有在使用者明確要求時才開。日常變更的 pull request 開在這個 fork，基底是 `origin/main`。
