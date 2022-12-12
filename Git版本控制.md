# Git版本控制
#### 進度
```
完成!!!
```
#### 數據庫(Repository)簡介
> Git的數據庫分為1.本地端數據庫。2.遠端數據庫。
```
本地端數據庫：為了方便用戶個人使用，在自己的機器上配置的數據庫。

遠端數據庫: 配有專用的伺服器，為了讓多人共享而建立的數據庫。

Git執行Push(推送)操作。執行Push之後，本地端的修改歷史會被上傳到遠端數據庫。

Git執行Pull(拉取)操作。執行Pull之後，遠端數據庫的修改歷史會下載到本地端數據庫。
```
#### HEAD
> HEAD 是一個指標，指向某一個分支，通常你可以把 HEAD 當做「目前所在分支」看待。也就是，現在在哪條 Branch上的哪個commit版本。
```
HEAD   = HEAD~0 = HEAD^0   當前提交

HEAD~  = HEAD~1 = HEAD^    上一次提交

HEAD~~ = HEAD~2 = HEAD^^   上兩次提交
```
#### 狀態訊息
```
Untracked files：代表尚未add加入追蹤，檔案所在區域為工作目錄。

Changes to be committed：已從工作目錄註冊至索引區，尚未提交。
```

#### 建立數據庫
> 建立本地端數據庫的方法有兩種：1.重新建數據庫。2.複製遠端數據庫。

#### 區域結構
```
#工作目錄區（Working Tree）是保存您目前正在處理檔案的目錄，Git 相關的操作都會在這個目錄下完成。

#索引區(Index)位於工作目錄區和本地端數據庫之間，是為了向本地端數據庫提交作準備的暫存區域。

#在工作目錄上做的任何變更並不會直接提交到數據庫的。Git在執行提交的時候，是將索引區的狀態儲存到數據庫。

#若想把變更與新增的檔案/目錄儲存到數據庫中，您需要執行提交（Commit）。

[工作目錄區] --註冊(add)--> [索引區] --提交(commit)--> [本地端數據庫] --推送(push)--> [遠端數據庫]          
```
#### 在本地端建立數據庫操作(所有操作皆在本地端)
```
1.在電腦上的任何一個地方建立XXX資料夾
2.資料夾右鍵Git Bash Here > $ git init  //將目錄建立為本地端數據庫。

3.加入一個新的abc.txt檔案
4.$ git stauts  //發現未加入索引(Untracked files:abc.txt)
5.$ git add abc.txt
6.$ git stauts  //發現已加入索引，但未提交(Changes to be committed: new file:   abc.txt)

7.$ git commit -m "first commit"
8.$ git commit
9.$ git status  //顯示沒有其他須提交(nothing to commit working directory clean)

10.$ git log  //確認一下數據庫的歷史提交記錄(commit的時間日期名稱)
```
#### 1.建立遠端數據庫(省略)

#### 2.建立遠端數據庫別名
```
$ git remote add <name> <url>
$ git remote add origin http://gitlab.asgaed.com.tw/ck/ims_fingate.git

--為遠端數據庫建立別名，以後push的時候就不需輸入冗長地址了。
--在主控台，執行push或pull命令時想省略遠端數據庫名稱的話，會使用origin名稱作為遠端數據庫。因此一般都會為遠端數據庫命名為origin。
```
#### 3.推送到遠端數據庫
```
$ git push <repository> <refspec>...
$ git push origin master

--如果是在複製的數據庫裡執行push命令時，您可以省略數據庫和分支的名稱。
```
#### 1.產生衝突過程
```
[UserA]
1.變更abc.txt內容:
add 修改加入索引
commit 記錄索引的狀態

2.$ git add sample.txt
  $ git commit -m "添加commit的說明"


[UserB]
1.變更abc.txt內容:
add 修改加入索引
pull 取得遠端數據庫的內容

2.$ git add sample.txt
  $ git commit -m "添加pull的說明"

3.$ git push


[UserA]
1.$ git push  //error: failed to push some refs to 
```
#### 2.解決衝突
```
[UserA] //先將最新的修改紀錄拉下來
1.$ git pull origin master  //CONFLICT (content): Merge conflict in sample.txt

2.開啟檔案，顯示衝突為:
連猴子都懂的Git命令
add 修改加入索引
<<<<<<< HEAD
commit 記錄索引的狀態
=======
pull 取得遠端數據庫的內容
>>>>>>> 4c0182374230cd6eaa93b30049ef2386264fe12a

3.解決衝突點，修正為:
連猴子都懂的Git命令
add 修改加入索引
commit 記錄索引的狀態
pull 取得遠端數據庫的內容

4.$ git add sample.txt
  $ git commit -m "合併"

5.$ git push
```
#### 分支簡介
* Integration分支 (亦可稱Master分支)
```
1.Integration分支是為了可以隨時建立發布版本的分支。

2.通常會將master分支當作Integration分支使用。
```
* Topic分支 (亦可稱Feature分支)
```
1.Topic分支是為了開發功能或修復錯誤之類的任務所建立的分支。

2.Topic分支是從穩定的Integration分支上建立的，完成作業後，要將Topic分支再合併到Integration分支。
```
#### Stash
> Stash是暫時儲存檔案修改內容的區域。Stash可以暫時儲存工作目錄還沒提交的修改內容，您可以在事後再取出暫時儲存的修改，應用到原先的分支或者其他的分支中。

> 現在你想切換分支，但是你還不想提交你正在進行中的工作；所以你儲藏這些變更。為了往堆疊推送一個新的儲藏，執行 git stash之後，你的工作目錄就乾淨了。
* 範例
```
在JeffBranch的abc.txt檔案，如果在未提交的情況下checkout到TomBranch，檔案內容會變成TomBranch上的。

但如果TomBranch的abc.txt檔案有做修改的話，checkout會失敗。這時必須要#先提交 or #將修改內容放到stash中暫時儲存，再checkout。
```
#### fetch
> 取得遠端數據庫的最新歷史記錄，但有別於pull，不會合併檔案，而是取得的提交會導入在自動建立的分支中，並可以切換這個名為 FETCH_HEAD 的分支。

> $ git pull = $ git fetch + $ git merge

#### 標籤(tag)
> 兩種類型的標籤：輕量標籤（lightweight tag）、附註標籤（annotated tag）
* 分支與標籤差異
```
分支會隨著 Commit 移動，而標籤則是固定留在某個 Commit 上。

分支會因為 commit 而往前，標籤則固定不動。

分支可以修改並作 commit，但標籤不會。

分支可以合併，但標籤則是獨立的。
```
* 指令
```
//新增一個輕量標籤，如果沒有指定哪個 Commit 時，Git 會自動指向最新的 Commit。
$ git tag [標籤名稱] 

//在特定的 Commit 上貼上輕量標籤
$ git tag [標籤名稱] [commit id]

//新增一個帶有附註資料的標籤
$ git tag [標籤名稱] [commit id] -a -m"輸入訊息參數" 

$ git tag third_tag e8a31c0 -a -m"example_tag" # 在 e8a31c0 這個 Commit 上加上 third_tag 標籤

//查詢標籤
$ git tag 

//查看標籤內容
$ git show [標籤名稱] 

//刪除特定標籤
$ git tag -d [標籤名稱] 
```


#### 合併(Merge & Rebase)
```
在Git，HEAD代表當前分支的最新提交名稱。在建立新的數據庫時，Git會預設HEAD指向master分支。

//兩條線匯合成一個新的節點
Merge: 匯合兩個修改時會產生一個名為「合併提交」的提交。Master的HEAD位置會被更新到新建立的合併提交上。

//bugfix分支的歷史記錄會增加在 master 分支的後面，歷史記錄會被統一，形成簡單的一條線。
Rebase: master 分支合併 bugfix 分支後，master 的HEAD會移動到 bugfix 的HEAD這裡。


Merge優劣: 修改內容的歷史記錄會維持原狀，但是合併後的歷史紀錄會變得更複雜。

Rebase優劣: 修改內容的歷史記錄會接在要合併的分支後面，合併後的歷史記錄會比較清楚簡單，但是，會比使用 merge 更容易發生衝突。
```
#### 基礎指令
```
//確認工作目錄與索引的狀態
$ git status

//確認數據庫的歷史提交記錄
$ git log

//確認數據庫的歷史提交記錄(壓縮資訊到一行)
$ git log --oneline

//查看目前本地分支 (前面有 * 的就是現在的分支，HEAD所在位置)
$ git branch

//查看遠端分支
$ git branch -r

//查看數據庫的所有紀錄
$ git reflog

//將檔案加入到索引區
$ git add <file>...

//表示可以把當前目錄下所有的檔案加入到索引區。
$ git add .

//提交訊息
$ git commit -m "write some message"


//人在A分支將JeffTest分支merge進來
$ git merge JeffTest

//本地端推送到遠端
$ git push


//複製遠端數據庫 到 本地端數據庫
$ git clone http://gitlab.asgaed.com.tw/ck/ims_fingate.git


//建立新分支
$ git branch JeffTest

//切換分支
$ git checkout JeffTest

$ git checkout [branch Name]/[commit id]

//建立新分支並同時切換分支
$ git checkout -b JeffTest

//推送到遠端儲存庫並建立新分支
$ git push --set-upstream origin JeffTest


//拉取本地端沒有的遠端分支到本地端
$ git checkout XXX遠端分支名


// 删除本地分支
$ git branch -d localBranchName

// 删除遠程分支
$ git push origin --delete remoteBranchName


衝突時:

add 修改加入索引
<<<<<<< HEAD (目前所在位置/線別)
commit 記錄索引的狀態
=======
pull 取得遠端數據庫的內容
>>>>>>> issue3 (要merge進來的線別)
```
#### git log 與 git reflog差異
```
???git log看的到跟版控網頁同樣的所有紀錄，git reflog看到的會有缺漏???

git log命令可以顯示當前分支所有提交過的版本信息，不包括已經被删除的 commit 
紀錄和reset的操作。(注意: 只是當前分支操作的信息)。

git reflog命令可以查看所有分支的所有操作紀錄信息
（包括已經被删除的 commit 紀錄和 reset 的操作）

git log 和 git reflog的最大區别是能不能查詢到被删除的 commit 紀錄和 reset 的操作紀錄，
log不能，而reflog可以；所以以後要買後悔藥就去找reflog。
```



#### 復原大法
```
Case1:還沒add加入追蹤，git checkout 可復原。

Case2:已經add加入追蹤，要先reset取消追蹤，再git checkout 復原。

Case3:已經add and commit，可使用$ git reset HEAD^ + $ git checkout .。
Case3:已經add and commit，可使用$ git reset --hard HEAD^。


// 取消已經commit但未push到遠端的動作
--相當於git reset --mixed HEAD^，意思是取消git commit及git add，但保留本地工作目錄的異動。--
$ git reset HEAD^


// 取消一個檔案add加入追蹤
$ git reset <file>

// 取消全部add加入追蹤
$ git reset


// 還原一個還沒有add文件的修改 
$ git checkout <file>

// 還原工作區所有還沒有add文件的修改
$ git checkout .


// 取消已經add or commit動作 + 檔案還原未修改前的狀態
$ git reset --hard HEAD^
```
#### 退版
```
本地退版到指定版本:
$ git reflog  //找到要回退的版本的commit id
$ git reset --hard 1fb0a257(commit id)  //回退版本

遠端退版到指定版本(以本地為主):
$ git reflog  //找到要回退的版本的commit id
$ git reset --hard 1fb0a257(commit id)
$ git push -f  //若有衝突,但確認要以本地為主,把遠端直接覆蓋　　


將遠端拉回本地端(以遠端為主)
$ git fetch --all  //取得所有branch
$ git reset --hard origin/master  //放棄目前所有檔案, 還原成遠端版本origin/master
$ git pull origin master  //重拉
```
#### 改寫提交
* 指令
```
//修改最近的提交訊息
$ git commit --amend

//取消過去的提交
$ git revert [commit id]

//刪除提交
$ git reset --hard [commit id]

//從其他的分支複製指定的提交，然後導入現在的主要分支
$ git checkout 主要分支
$ git cherry-pick 其他分支[commit id]

//合併過去的提交(Ex:兩個提交合併成一個提交)
$ git rebase -i HEAD~~

//在主要分支上新建一個匯合所有提交的提交
$ git checkout 主要分支
$ git merge --squash 其他分支[commit id]
```
* reset和revert差別
```
reset: 
1.回退到某個版本
2.git reset 是把HEAD向後移動了一下
3.把某些commit在某個branch上刪除，但要注意和老的branch再次merge時，這些被刪除的commit還是會被再次引入

revert: 
1.取消過去所發布的提交
2.是用一次新的commit来抵銷之前的commit
3.git revert是HEAD繼續前進

假如有三個提交，a-->b-->c(head-->master)：
1、reset b變為：a-->b；
2、revert b變為：a-->c。
```
