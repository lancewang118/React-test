#Git 入門

##Git基本介紹
**Git** 是一個分散式版本控制軟體，最初由林納斯·托瓦茲創作，於2005年以GPL釋出。最初目的是為更好地管理Linux核心開發而設計。 [維基百科](https://zh.wikipedia.org/wiki/Git)  
  
###基本指令
```
$git --version  	//顯示git 版本
```
![git version](https://github.com/lancewang118/React-test/blob/master/git_version.png)
  
首先先建立 本地端(Local)的 Repository。
  
```
$mkdir test			//先建立目錄
$cd test			//進入到test 目錄
$git init			//在此目錄下做初始化
```
```
$git add file   //增加檔案但尚未提交
$git status     //顯示目前工作區狀態
```
![git version](https://github.com/lancewang118/React-test/blob/master/git_add_status.png)
  
```
$git rm --cache file    	//移除尚未提交(commit)的檔案
$git status					//來看一下目前狀態
```
![git version](https://github.com/lancewang118/React-test/blob/master/git_rm_status.png)
