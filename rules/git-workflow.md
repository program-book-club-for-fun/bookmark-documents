# Git Workflow

此文件會說明 `bookmark` 系列 repository 中應遵守的 Git 開發流程，包括：

* Commit 守則
* Branch 守則

## Commit 守則

主要有兩點說明：

### commit 內容

- 單一職責 ( 除非有 typo 之類的 minner fix )
- 要能正常執行

### commit log

* 盡量保持一行，除非有一些太 minner 的 fix
* 多行的話，第一行要寫最重要的 (或是大綱)
* 格式：`[[commit type]] your logs here`
  * Commit 種類：
    * `[feature]`：commit 內容為新功能
    * `[fix]`：commit 內容為修正 Bug
    * `[refactor]`：commit 內容為重構
    * `[add]`：commit 內容為新增 API 或函式庫等
    * `[remove]`：commit 內容為刪除 API 或函式庫等
    * `[update]`：commit 內容為更新函式庫等
    * `[MISC]`：commit 內容為微小修改 ( 例如 typo )
  * 須為全英文
  * e.g `[add] add git-workflow.md`

## Branch 守則

參考 [git flow](http://nvie.com/posts/a-successful-git-branching-model/)，但有一些不同點：

主要只有三種分支：

* master 分支
* develop 分支
* issue 分支

### master 分支

為主要 release 的分支。只有在確定版本可以上線，且非常穩定的狀況下，才可從 develop 分支合併進來。這裡的 master 分支可想成是 git flow 中的 master 分支與 release 分支的綜合體。

應遵守的事項為：

* 不可在 master 上開發
* 只能與 develop 分支合併
* 每個由 develop 分支合併進入後的版本都應標上 release tag ( 除非突然需要 Hotfix )

### develop 分支

為一切開發的基底分支。是從 master 分出去且一直存在的分支。只有在 issue 分支做完並通過 pull request 後，才可從 issue 分支合併進來。當 master 分支需要 hotfix 時，develop 分支也是 hotfix issue 的基底分支。這裡的 develop 分支可想成是 git flow 中的 develop 分支與 hotfix 分支的綜合體。

應遵守的事項為：

* 不可在 develop 上開發 ( 除非很 minner 的改動 )
* 所有的 issue 分支都要由 develop 當前的 HEAD 分出去開發
* 只能與 issue 分支合併
* 當需要 Hotfix 時，也是從 develop 分支分出 issue 分支 ( 或者直接使用需要 hotfix 的 issue 分支 )，解完合併回 develop 分支，確定穩定後再合併回 master 分支

### issue 分支

為主要開發分支。開發前要先開一個 issue，並開對應的 issue 分支 。做完 issue 並通過 review 後就可合併為 develop。這裡的 issue 分支可想成是 git flow 的 feature 分支。

應遵守的事項為：

* 開分之前應該對應的 issue
* 由 develop 當前的 HEAD 分出去開發
* 只能合併回 develop
* 命名格式：`[issue-number]-issue-name`
  - 開頭為 issue 號碼
  - 須為全英文
  - 字中間以 `-` 區隔
  - e.g： `1-Set-git-workflow-rule`

