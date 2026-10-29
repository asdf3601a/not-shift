# 代理開發約定

這個 repository 是個人 fork [`asdf3601a/not-shift`](https://github.com/asdf3601a/not-shift)。上游是 [`JasonHsuFet/Working_Shift`](https://github.com/JasonHsuFet/Working_Shift)，預設分支是 `main`。

## 每次開發之前

先同步上游，再改程式。不要在 `main` 上直接開發。

1. 確認 `upstream` remote 存在。沒有就加上，且只對它 fetch，不要 push：

   ```bash
   git remote get-url upstream >/dev/null 2>&1 || git remote add upstream https://github.com/JasonHsuFet/Working_Shift.git
   git fetch upstream --prune
   ```

2. 比較 `upstream/main` 與 fork 的 `origin/main`。用 `git log origin/main..upstream/main` 列出上游多出來的提交，並用 `git diff --stat origin/main...upstream/main` 看影響的檔案。也檢查反方向 `upstream/main..origin/main`，指出 fork 自己多出來的提交。

3. 在開始改程式之前，先給使用者一份繁體中文摘要。沒有新提交也要明講，並寫出兩邊共同的提交。摘要包含提交、時間（Asia/Taipei）與受影響的路徑，不要只寫「已同步」。

4. 從包含這次上游更新的起點開獨立分支再開發。
   - `upstream/main` 有 fork 尚未包含的提交時，在工作分支上 `git merge upstream/main`，不要把合併直接推上 `main`，也不要 force-push `main`。
   - Cloud Agent 的分支名稱遵循該次工作要求的格式。
   - 對上游的 pull request 只有在使用者明確要求時才開。日常變更的 pull request 開在這個 fork。
