## コンフリクトを理解し、解消する練習

### 参考文献
- [マージ競合について](https://docs.github.com/ja/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/about-merge-conflicts)
- [Gitのコンフリクトを解消する手順](https://udemy.benesse.co.jp/development/system/git-conflict.html#:~:text=%E3%82%B3%E3%83%B3%E3%83%95%E3%83%AA%E3%82%AF%E3%83%88%E3%81%A8%E3%81%AF%E3%80%81Git%E3%81%A7,%E3%81%AA%E3%81%A9%E3%81%AF%E8%B5%B7%E3%81%8D%E3%81%BE%E3%81%9B%E3%82%93%E3%80%82)
- [マージ・リベースとコンフリクト](https://youtu.be/CWhOG2mSjqQ?si=tjhhwI4kyYvqzIAb)
- [リベースでのコンフリクト解消方法](https://youtu.be/bFQ4EjCu4iE?si=ERzii74m9sZu6bMe)
- [CUIベースの解説](https://youtu.be/V7WAxif7yT4?si=vAc7whtBVAGdE33I)
- [リベースでマージする](https://backlog.com/ja/git-tutorial/stepup/13/)
- [リベースの具体的なメリット](https://zenn.dev/tana0102/articles/475d8952933af6)

### 概要
このリポジトリはGitのコンフリクトを意図的に発生させ、その解決方法を学ぶための練習用リポジトリです。

### 初期ファイル
このリポジトリには以下のファイルが含まれています。
- README.md - このファイル
- members.txt - チームメンバーリスト（ここにメンバーを追加）

### 準備
1. このリポジトリクローンして、フォルダをエディターで開きます。
```bash
# リポジトリをクローン
git clone https://github.com/shige-99/resolve-conflict.git

# フォルダに移動
cd resolve-conflict
```

2. 各自のローカル環境でブランチを作成してください。
```bash
   # 新しいブランチを作成
   git checkout -b 自分の名前-branch
```

### コンフリクトを発生させる手順

1. 全員が同じファイルの同じ行を編集します。
   ```bash
   #　作成したブランチにいることを確認できたら・・・
   
   # members.txtを編集（同じ行に自分の名前を追加）
   echo "1. 自分の名前" >> members.txt
   
   # 変更をコミット
   git add members.txt
   git commit -m "自分の名前を追加"
   
   # リモートにプッシュ
   git push origin 自分の名前-branch
   ```

2. 最初のメンバーがプルリクエストを作成し、mainブランチにマージします。

3. 次のメンバーがプルリクエストを作成すると、コンフリクトが発生します。

### コンフリクトの解決方法
コンフリクト解消方法には主に以下の二つの方法がある。
1. マージ(git merge)
2. リベース(git rebase)
3. リモートリポジトリ上でコンフリクトを解消(チーム開発では非推奨)

※どちらもメリット・デメリットがある。
個人的な結論は下記の使い方がベストだと思っているが、現場のルールによって変わるので全て使用できるようにしておくことがベスト。

- チーム開発や本番リリースの統合 → `git merge`
- 個人の作業ブランチの更新 → `git rebase`
- 個人だけで使うリポジトリ → GitHub の PR 画面で解決

> [!NOTE]
> [merge派、rebase派の記事](https://style.biglobe.co.jp/entry/2022/03/22/090000)  

#### 1. マージ(git merge)で解消する方法

1. 最新のmainブランチを取得
   ```bash
   git checkout main
   git pull origin main
   ```

2. 自分のブランチに戻り、mainをマージ
   ```bash
   git checkout 自分の名前-branch
   git merge main
   ```

3. コンフリクトが発生したら、ファイルを開いて確認します
   ```
   # チームメンバーリスト
   <<<<<<< HEAD
   1. 自分の名前
   =======
   1. 先にマージされた人の名前
   >>>>>>> main
   ```

4. ファイルを編集してコンフリクトを解決します
   ```
   # チームメンバーリスト
   1. 先にマージされた人の名前
   2. 自分の名前
   ```

5. 解決したファイルをコミット
   ```bash
   git add members.txt
   git commit -m "コンフリクトを解決"
   git push origin 自分の名前-branch
   ```

6. プルリクエストを更新し、マージします。

#### 2. リベース(git rebase)で解消する方法

1. 最新のmainブランチを取得
   ```bash
   git checkout main
   git pull origin main
   ```

2. 自分のブランチに戻り、mainをリベース
   ```bash
   git checkout 自分の名前-branch
   git rebase main
   ```

3. コンフリクトが発生したら、ファイルを開いて確認します

4. ファイルを編集してコンフリクトを解決します

5. 解決したファイルをコミット

6. プルリクエストを更新し、マージします。

### コンフリクトを未然に防ぐための仕組み
- 同じファイルに対して並行開発をしない。
- ファイルを常に最新の状態にする。
- 小さなコミットを心がける。
- ブランチ戦略の活用
- コミュニケーションの徹底

etc...





