# Your Schedule
[ページはこちら](https://cal-frontend.vercel.app/)

こちらはNext.jsによるフロントエンド側のAppレポジトリーです。
**バックエンド**側のRails API側のレポジトリーは[こちら](https://github.com/takaya787/cal_backend)

## サイト概要

**Your Schedule**はあなたのスケジュール帳をウェブ上に作成できます。<br>

## 作成理由　
カレンダーで、予定を管理することと同時に、タスク管理もできるようにしたかった。

## 使用技術

* Ruby 2.7.2, Rails 6.0.3
* React
* Next.js
* Docker, Docker-compose (開発環境)
* Postgresql(DB)


## 機能一覧
**【機能一覧】**

◆　ユーザー機能 
* 新規登録、ログアウト

◆　イベント機能 
* イベントの新規作成、削除

◆　タスク機能
* タスクの新規作成、削除
* タスクの完了済みかどうかを記録
* タスクの状態毎に表示を変える

## こだわった点
### 今回特にこだわった点は**非同期通信の快適さ**です。
各userの作成したイベント情報、タスク情報は全てbackend側のデータベースに保存され、それらのデータをclient側で取得して、表示させています。
僕が特にこだわった点は、ユーザーの行った変更がすぐにユーザーに見える形で適用されることです。

### 非同期通信にSWRを使用

いくつかの異なるcomponentsで、非同期通信の情報をラグが少なく共有するための手段として、**SWR**を使用しています。
**SWR**は情報の共有、更新を一括で管理する事ができるので、
今回のサイトでは、投稿の**作成、削除**、タスクに関しては**完了情報の変更**まで、データベースの変更を時差なくclient側に表示できるようにしています。

### SWRのメリット

reduxとredux-sagaでの状態共有と比べて、圧倒的に簡単に共有でき、またデータの更新も関数一つで行える点は非常に便利です。