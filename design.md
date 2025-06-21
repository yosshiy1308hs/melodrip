# 音楽共有SNSアプリ 設計書

## 1. システム構成

- フロントエンド：React（Next.js推奨）、TypeScript
- バックエンド：Node.js（Express）、TypeScript（必要に応じて）
- 認証：Firebase Authentication（メールアドレス/SNS連携）
- データベース：Firebase Firestore
- ストレージ：Firebase Storage（アイコン画像保存用）
- 外部API：YouTube Data API等（タイトル・アーティスト取得用）

## 2. 主要画面設計

### 2.1. 認証・ユーザー管理
- サインアップ/ログイン画面（Firebase Authentication利用）
- プロフィール編集画面（アイコン画像アップロード、Firebase Storage利用）

### 2.2. 投稿関連
- 投稿一覧画面（カード型、タイトル・アーティスト・サムネイル表示、いいねボタン）
- 新規投稿画面（外部リンク入力のみ、プレビュー表示）
- 検索画面（タイトル・アーティスト名でフィルタ）

### 2.3. 管理者画面
- 投稿一覧（削除ボタン付き、不適切投稿の管理）

## 3. データベース設計（Firestoreコレクション例）

### users
| フィールド         | 型         | 説明                |
|--------------------|------------|---------------------|
| uid                | String     | FirebaseユーザーID   |
| email              | String     | メールアドレス      |
| displayName        | String     | 表示名              |
| iconUrl            | String     | アイコン画像URL     |
| createdAt          | Timestamp  | 登録日時            |

### posts
| フィールド         | 型         | 説明                |
|--------------------|------------|---------------------|
| id                 | String     | 投稿ID              |
| userId             | String     | 投稿者ユーザーID    |
| musicUrl           | String     | 外部リンクURL       |
| title              | String     | 曲タイトル          |
| artist             | String     | アーティスト名      |
| thumbnailUrl       | String     | サムネイル画像URL   |
| likeCount          | Number     | いいね数            |
| createdAt          | Timestamp  | 投稿日時            |

### likes
| フィールド         | 型         | 説明                |
|--------------------|------------|---------------------|
| id                 | String     | いいねID            |
| userId             | String     | いいねしたユーザー  |
| postId             | String     | 投稿ID              |
| createdAt          | Timestamp  | いいね日時          |

## 4. API設計（例）

- Firebase Functions（必要に応じて）
- Firestore直接操作（クライアントから）
- YouTube Data API連携（クライアントまたはFunctions経由）

## 5. 外部サービス連携

- YouTube Data API等でリンクからタイトル・アーティスト・サムネイルを自動取得

## 6. UI/UX

- モバイルファーストのレスポンシブデザイン
- 若者向けのカラフルで直感的なUI
- 投稿カードはサムネイル・タイトル・アーティスト・いいねボタンを表示
