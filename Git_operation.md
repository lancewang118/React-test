# Git 入門

## Git基本介紹
**Git** 是一個分散式版本控制軟體，最初由林納斯·托瓦茲創作，於2005年以GPL釋出。最初目的是為更好地管理Linux核心開發而設計。 [維基百科](https://zh.wikipedia.org/wiki/Git)  

**本地端版本管理**  
![RCS](https://github.com/lancewang118/React-test/tree/master/image/RCS.png)  

**集中式版本管理**  
![VCS](https://github.com/lancewang118/React-test/tree/master/image/CVCS.png)  

**分散式版本管理**  
![DVCS](https://github.com/lancewang118/React-test/tree/master/image/DVCS.png)  

### 設定環境
利用git的工具 git config能夠取得和設定參數，這參數存放在下列三個位置：  

* /etc/gitconfig： 所有使用者預設設定，使用參數 --system。
* ~/.gitconfig、~/.config/git/config： 帳號使用者 專用設定。 使用參數 --global
* .git/config：Repository 專用的設定。
* 優先權： Repository > user > all.

在Windows系統中，通常會 C:\Users\$USER 或是 C:\ProgramData\Git\config，要修改需有管理都權限執行 **git config -f <file>**。  

### 設定使用者帳號及E-mail
使用 --global則此使用者登入此系統中，Git 都採用此資訊。若是特定專案使用，只需在專案目錄下執行 **git config user.name** 及 **git config user.email** ，不加 --global。

```
$git config --global user.name "Ho Liu Ken"
$git config --global user.email holiuken@streetfighter.com
//專案用
$git config user.name "Ho Liu Ken"
$git config user.email holiuken@streetfighter.com
```

### 設定編輯器

預設情況下，Git會使用系統預設的編輯器，若想使用不同的，可以用下列指令：  


`$git config --global core.editor emacs`

Windows：

```
// x86 system：
C:\>git config --global core.editor "'C:\Program Files\Notepad++\notepad++.exe' -multiInst -nosession"

//x64 system：
C:>git config --global core.editor "'C:\Program Files(x86)\Notepad++\notepad++.exe' -multiInst -nosession"
```

### 查看設定

若想知道目前設定資料，可以使用 **git config --list** 。

```
$git config --list --local		//local 此目錄下的 .gitconfig
$git config --list --global	//  Users/username/.gitconfig
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.ra.url=https://github.com/lance/React-test
remote.ra.fetch=+refs/heads/*:refs/remotes/ra/*
user.name=lance
user.email=m@gmail.com
```

### 說明文件

若在使用上需要幫助，有三種方法可以取得：

```
$git help <command>
$git <command> --help
$man git-<command>

example：
$git help config	//取得config的說明文件
```

### Git Version

```
$git --version  	//顯示git 版本
git version 2.23.0
```
  

## 基本指令
首先要了解Git 專案的三個狀態：git 資料夾、工作目錄(working)及預存區(staging)。  

![git version](https://github.com/lancewang118/React-test/blob/master/image/Status.png)


  
### 建立Git repository
兩種方法可以建立Git Repository，第一種在現有專案下的本地端(Local)的 Repository。
  
```
$cd test			//進入到test (專案資料夾下)
$git init			//在此目錄下做初始化
```

此時會在test下建立 .git的子目錄及其所必要的檔案。  

```
$git add .		//將目前目錄內的所有檔案加入staged.
$git add test.js	//只加test.js 進入 staged.
$git commit -m 'initial project version'		//提交在staged 的檔案
```

第二種方式為取得Git repository的複本，它會將遠端Repository 的每個檔案的每個版本都取回來。  

```
$git clone https://gihub.com/ho-liu-ken/fist	//這會建立一個fist 資料夾
$git clone httpe://github.com/ho-liu-ken/fist myFist	//clone 遠端fist project 到本地的 myFist資料夾
```

### 檢查檔案狀態
工作目錄下的每個檔案只有兩種狀態：已追蹤(tracked)、未追蹤(untracked)。在tracked中的檔案狀態可能為：未修改(Unmodified)、已修改(modified)、已預存(staged)；未追蹤則是在工作目錄下但不在上次的快照(snapshot)及 staged area內的檔案。  

![File_status](https://github.com/lancewang118/React-test/tree/master/image/file_status.png)

**git status** 用來檢查檔案處在什麼樣的狀態下。  


```
$git status     //顯示目前工作區狀態
On branch master	//分支 master
nothing to commit, working tree clean		//目前工作目錄是 clean
```

假設在工作目錄內編輯一個檔案並新增一個檔案，然後我們再來看一下git status 的變化。

```
$git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   Creating a React App.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file_status.png

no changes added to commit (use "git add" and/or "git commit -a")
```

* Untracked files: 顯示的是不在上次snapshot內的檔案，可以用命令 **git add** 或 **git commit -a**來加入 track。
* modified：顯示的是已追蹤的檔案但被修改了。


```
$git add 'Creating a React App.md'
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   Creating a React App.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file_status.png
```
* Changes to be committed：當我們使用 **git add file** 時，檔案就會進入staged area。

```
$git commit -m 'change react contents'	//將staged file commit 提交
[master 8376d35] change React contents
 Committer: cml <flow@cml>
 1 file changed, 3 insertions(+)
 
$git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file_status.png
```

當我們使用 **git commit -m 'change content'**，git 就會更新檔案snapshot，此時我們只剩新檔案還處於untracked 狀態。

### git status -s  or git status --short

使用 -s 參數時，輸出會變得比較簡單的內容，左邊欄位是指 **預存區** 狀態，右邊欄位是 **工作區** 狀態。  

* ??：未追蹤的新檔案(untracked files).
* A： 加入預存區的檔案
* M：已修改的檔案

```
$git status -s
?? file_status.png
```

### 忽略不要的檔案 ( .gitignore)

如果有不想要被git 自動加入的檔案，也不顯示在 untracked files，可以建立一個 **.gitignore** 的檔案，在裡面加入不想要被追蹤的檔名的規則，那符合這規則的檔案就不會被列入追蹤了。

* 空白或者以 # 開頭 會忽略這列的內容
* /結尾：代表目錄
* /開頭：避免路徑遞迴
* !開頭：規則反向
* Glob模式：簡化版的 regular expressions
	* (星號) *：符合零或多個字元
	* (問號) ?：符合一個字元
	* [abc]：符合a、b、c 其中一個
	* [0-9]：符合0-9的其中一個數字
	* (星星) **：可以用來多層目錄
	
	
```
#不要追蹤所有副檔名為 log的檔案.
*.log

#忽略根目錄下的 abc 檔案，但不含子目錄下的 abc 檔案
/abc

# ignore node_modules/ 目錄下所有檔案
node_modules/

#忽略 pdf，忽略report/內的pdf，但不包含 report/a/a1.pdf
report/*.pdf

# 多層目錄 忽略report/ 目錄下的所有 pdf及doc，包含 report/a/a1.pdf
report/**/*.pdf
report/**/*.doc
```


### 檢視tracked file已修改但未add to staged 的內容( git diff)

想要知道修改檔案與追蹤的檔案的內容差異，可以使用 **git diff**，比較的是tracked file與working area中modified file的內容，若是進行 git add file進staged 後再執行 git diff是看不到內容的。若是要查看 tracked與在staged內的內容差異可以加上參數 **git diff --staged**  或 **git diff --cached**。

```
$git diff		//會顯示修改位置上三行及下三行內容
diff --git a/Creating a React App.md b/Creating a React App.md
index 115cfe3..d8ab0f2 100644
--- a/Creating a React App.md   
+++ b/Creating a React App.md   

-### React
+
 
 React Component
 
@@ -63,6 +63,7 @@ $npm install --save react react-dom react-router
 
 ### Redux
 
+State Store
 
 $npm install --save redux react-redux react-router redux-actions redux-thunk
```

* -：代表修改的檔案與上次比較 *被刪除的內容*
* +：代表修改的檔案與上次比較 *新增加的內容*

### Git Commit 提交

當使用git add 將修改或新增的檔案加入到 staged area，並不會產生新的snapshot，而是要再使用 **git commit** 將staged area的檔案提交出去，此時才會更新檔案snapshot，常用參數如下：

* -m：輸入提交訊息，若沒使用這參數，會啟editor 編輯提交訊息。
* -a：略過 git add 這一步驟。(會把modified files 都提交出去)
* -v：editor 會顯示出修改的內容差異。

```
$git commit -a -m 'Added Redux content'
[master bb6acd3] Added Redux content
 1 file changed, 1 insertion(+)
```

成功後會看到一些訊息，首先master是指目前的分支；bb6acd3則是指 SHA-1 校驗碼；Added Redux content則是提交訊息，一個檔案修改，增加一行內容。

### Git rm 移除檔案

要從 Git 中刪除檔案，不能只是將working area的檔案刪除，而是要將其從 Git 的tracked file移除，此時可以使用 **git rm**來完成，它會移除 tracked file及刪除在working area的檔案，如此也不會列在untracked file。  

```
$git rm 'Creating a React App.md'		//將檔案加入到 staged area，但working area已刪除此檔案
$git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    Creating a React App.md
$git commit							//commit後連同git tracked file記錄也移除
//在還沒commit前，可以救回檔案.
$git restore --staged 'Creating a React App.md'	//先將其移出staged area.
$git restore 'Creating a React App.md'			//此時 Git會從前一snapshot將檔案複製回來，可從檔案的建立時間
```

### Git mv 檔名變更

要在 Git 中變更檔名，可以使用此命令 **git mv**。  

```
$git mv 'Creating a React App.md' Creating-React-App.md
$git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    Creating a React App.md -> Creating-React-App.md
```

可以看到在staged area內容是：renamed:    Creating a React App.md -> Creating-React-App.md，雖然還需要 git commit將 Git tracked file 變更內容生效，但看working area的檔案已先改為 Creating-React-App.md，所以實際上 **git mv** 相當於執行：

```
$mv 'Creating a React App.md' Creating-React-App.md
$git rm 'Creating a React App.md'
$git add Creating-React-App.md
```

### Git log 查看提交的歷史記錄

當想要查詢之前變更過什麼或是新加入一個專案需要知道之前的變更記錄時，可以使用 **git log**這項命令。它會以反向的時間順序列出提交過的歷史記錄，如SHA-1校驗碼、作者、提交日期、提交訊息。常用參數如下：  


* -p：顯示每筆提交所做的修改內容。
* -1,2：顯示最近1,2筆的資料。
* --state：簡略的提交資訊。
* --graph：輸出的日誌旁邊顯示分支及合併歷史的 ASCII 圖形。
* --pretty：改變預設的輸出格式
	* short：
	* oneline：
	* full：
	* fuller：
	* format：


**Example：git log**

```
$git log
commit a5a1d7871727d796b2472ff8286b77dbd6958a7b (HEAD -> master)
Author: cml <flow@cml>
Date:   Mon Jan 20 21:46:47 2020 +0800

    change file name

commit bb6acd3898742a8ad9c89cde7ab8f4b39c8c9a74
Author: cml <flow@cml>
Date:   Mon Jan 20 21:13:34 2020 +0800

    Added Redux content

commit 8376d35166cd6aca876615f744d08fa81d0f934c
Author: cml <flow@cml>
Date:   Mon Jan 20 19:27:22 2020 +0800

    change React contents
```

**Exampel： git log -p -2**

```
$git log -p -2
commit a5a1d7871727d796b2472ff8286b77dbd6958a7b (HEAD -> master)
Author: cml <flow@cml>
Date:   Mon Jan 20 21:46:47 2020 +0800

    change file name

diff --git a/Creating a React App.md b/Creating-React-App.md
similarity index 100%
rename from Creating a React App.md
rename to Creating-React-App.md

commit bb6acd3898742a8ad9c89cde7ab8f4b39c8c9a74
Author: cml <flow@cml>
Date:   Mon Jan 20 21:13:34 2020 +0800

    Added Redux content

diff --git a/Creating a React App.md b/Creating a React App.md
index 115cfe3..d8ab0f2 100644
--- a/Creating a React App.md   
+++ b/Creating a React App.md   
@@ -63,6 +63,7 @@ $npm install --save react react-dom react-router
 
 ### Redux
 
+State Store
``` 

**Example： git lot --state -2**

```
$git log --state -2
commit a5a1d7871727d796b2472ff8286b77dbd6958a7b (HEAD -> master)
Author: cml <flow@cml>
Date:   Mon Jan 20 21:46:47 2020 +0800

    change file name

 Creating a React App.md => Creating-React-App.md | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

commit bb6acd3898742a8ad9c89cde7ab8f4b39c8c9a74
Author: cml <flow@cml>
Date:   Mon Jan 20 21:13:34 2020 +0800

    Added Redux content

 Creating a React App.md | 1 +
 1 file changed, 1 insertion(+)
``` 

**Example： git log --pretty=oneline**

```
$git log --pretty=oneline -3
a5a1d7871727d796b2472ff8286b77dbd6958a7b (HEAD -> master) change file name
bb6acd3898742a8ad9c89cde7ab8f4b39c8c9a74 Added Redux content
8376d35166cd6aca876615f744d08fa81d0f934c change React contents
```

**Example： git log --pretty=format:"%s %an"**  
format 選項：  

* %H：提交 SHA-1 雜湊值。
* %h：提交簡短的 SHA-1 雜湊值。
* %T：「樹(tree)」物件的 SHA-1 雜湊值
* %t：「樹」物件簡短的 SHA-1 雜湊值
* %P：親代(parent)提交的 SHA-1 雜湊值
* %p：親代提交簡短的 SHA-1 雜湊值
* %an：作者名字。
* %ae：作者 E-mail。
* %ad：作者日期。
* %ar：作者日期，相對時間格式。
* %cn：提交者名字。
* %ce：提交者 E-mail。
* %cd：提交者 日期。
* %cr： 提交者 日期，相對時間格式。
* %s：提交訊息。


**Filter**

* --since,--after：特定日期後
* --until,--before：特定日期前
* --author：作者名字符合
* --committer：提交者名字符合
* --grep：提交訊息符合
* -S：修改檔案中有加入或移除指定字串

```
$git log --pretty=format:"%h - %s - %an - %ad - %cn - %cd" --since="2020-01-18"
a5a1d78 - change file name - cml - Mon Jan 20 21:46:47 2020 +0800 - cml - Mon Jan 20 21:46:47 2020 +0800
bb6acd3 - Added Redux content - cml - Mon Jan 20 21:13:34 2020 +0800 - cml - Mon Jan 20 21:13:34 2020 +0800
8376d35 - change React contents - cml - Mon Jan 20 19:27:22 2020 +0800 - cml - Mon Jan 20 19:27:22 2020 +0800
b34fb0b - fix bug - cml - Sun Jan 19 15:59:08 2020 +0800 - cml - Sun Jan 19 15:59:08 2020 +0800
6d4f8de - initial project - cml - Sun Jan 19 15:46:01 2020 +0800 - cml - Sun Jan 19 15:46:01 2020 +0800
```

## Git Remote 遠端操作

通常 Git 在本地端之外，專案為了能和其它人協同工作，會有一個放在網路上共用的 Repository。  

** Git remote

Git remote 可以檢視目前設定好的遠端專案位置及別名，例如 origin 是當使用 **git clone** 時，Git 預設
的簡稱。  

```
$cd test	//到專案目錄下
$git remote
origin
```

### Git remote add/rm 新增/移除遠端 repository

使用命令 **git remote add/rm 簡稱 url** 來新增或是移除遠端repository 連結。

```
$git remote add tes https://github.com/lance/test
$git remote
ra
tes
$git remote -v
ra	https://github.com/lance/React-test (fetch)
ra	https://github.com/lance/React-test (push)
tes	https://github.com/lance/test (fetch)
tes	https://github.com/lance/test (push)
$git remote rm tes
$git remote -v
ra	https://github.com/lance/React-test (fetch)
ra	https://github.com/lance/React-test (push)
```

### Git Clone / fetch / pull / push

當使用 **git clone**時， Git 會自動建一個相同的資料夾，並將遠端檔案都下載回來，同時會自動地將本地分支master 設為追蹤
遠端上的分支，

```
$git clone url
Cloning into 'React-test'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (15/15), done.
remote: Total 16 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (16/16), done.
$git status
On branch master
Your branch is up to date with 'origin/master'.		//注意，這邊和本地建立的資訊不同 origin/master

nothing to commit, working tree clean
```

當使用**git fetch**時，Git 會取得在clone 之後被推送到伺服器上的新的檔案，**但是 git fetch 只下載資料，不會自動合併，必須自己用手動方式進行合併**


如果目前的分支(branch)有設定追蹤遠端上的分支，當使用**git pull**時， Git 會自動獲取並合併 遠端分支資料到本地分支裡。

```
$git pull
Updating a2f1bb8..54b6487
Fast-forward
 Creating-React-App.md | 77 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 77 insertions(+)
 create mode 100644 Creating-React-App.md
```

當在本地專案完成之後，想要推送到遠端伺服上面去，這是就要使用 **git push remote-name local-branch-name**，這是 Git就會將已更新的檔案上傳過去。在沒有其他使用者更新過專案前，這命令能成功更新遠端 Repository；若是其他使用者有先更新專案內容而你的本地專案還沒更新，此時會被拒絕，你需先取得更新的專案內容並合併到你之前的工作內容裡，才能push 到遠端 repository。

```
$git push origin master
Username for 'https://github.com': 		//輸入使用者名稱
Password for 'https://Username@github.com': 		//輸入密碼
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 328 bytes | 328.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/lance/React-test
   54b6487..a06eba3  master -> master
```

### Git remote show

當要想對特定的遠端 Repository查看較詳細的資訊時，可以使用 **git remote show remote-name**。其中所顯示的訊息：  

* **HEAD branch：**目前本地分支。
* **Remote branch：**已追蹤的遠端分支。
* **git pull：**使用 git pull 時，會將遠端追蹤分支(remote master)合併到本地分支(master)。
* **git push：**使用 git push 時，會將本地分支(master)合併到遠端追蹤分支(master up-to date)。

```
$git remote show origin
* remote origin
  Fetch URL: https://github.com/lance/React-test
  Push  URL: https://github.com/lance/React-test
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```