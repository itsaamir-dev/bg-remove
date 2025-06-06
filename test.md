# ■ 設計メモ - 【SaaS 共通サービス】{画面/機能名}

## 実現すること
- ユーザーの詳細を閲覧でき、更新ができる


## 作業リポジトリ
- リポジトリ名: smo-spa-portal

### 段階対応計画

- plandevelop
  - 新規画面作成

## アクセス制限
- 閲覧/編集可能なロール
  - SERVICER, OWNER, CUSTOMER

## アクセス
- アクセス方法
  - アバターメニューから`ユーザ情報`をクリック 

## パフォーマンス設計（必要な場合）
なし

## URL
| URL | 説明 |
| --- | --- |
| /profile/user | ユーザーの詳細を閲覧でき、更新ができる |

## エラー表示について
- インプット項目下部に表示
  - 例） ユーザ名を入力してください

## APIエラー処理
- 401 ・・ リフレッシュトークンを更新して、処理を継続する
- 403・・「アクセス権がありません」（画面遷移しない）
- 400・・入力エラーが発生しました。」リクエストボディのフィールド名を返却して、列挙して表示する。（画面遷移しない）
- 422・・「再処理してください」（画面遷移しない）
- 429・・リトライ [共通仕様参照] ([URL](https://ogis-qasst.cloudmine.jp/projects/smoother/repository/docs/entry/02.%E5%9F%BA%E6%9C%AC%E8%A8%AD%E8%A8%88/01.SaaS%E5%85%B1%E9%80%9A%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9/%E3%83%90%E3%83%83%E3%82%AF%E3%82%A8%E3%83%B3%E3%83%89/WebAPIs/%E5%85%B1%E9%80%9A_%E8%A8%AD%E8%A8%88%E3%83%A1%E3%83%A2.md))
- それ以外の4XX・・「通信エラーが発生しました」（画面遷移しない）
- 500・・共通のエラー（フォールバック）画面を表示させてセッションを破棄
- Show the error Message in snackbar 

## 管理ポータル 国際化対応
- 多言語対応方法
  - (例) `src/config/lang/ja.json` を読み込む

## APIリクエスト

### 利用API 一覧

| Method | アクション | パス | 説明 |
| --- | --- | --- | --- |
| `GET` | 取得 | /userpools/self/user | ユーザー情報取得 |
| `PUT` | 更新 | /userpools/self/user | ユーザー情報更新 |


### リクエストヘッダ

| ヘッダ名 | 内容 | 説明 |
| --- | --- | --- |
| Authorization | Bearer <token> | 固定値「Bearer 」+ JWTアクセストークン |
| Content-Type | application/json | JSONデータ |

## ユーザー情報 画面

### ブラウザタブタイトル
ユーザー情報 | smoother管理ポータル

### 画面構成

| 項目名 | 種別 | 説明 |
| --- | --- | --- |
| ユーザー情報  | タブ | ユーザ情報タブを表示 |
| 詳細情報1  | タブ | 詳細情報1タブを表示 |
| 詳細情報2  | タブ | 詳細情報2タブを表示 |

### ユーザー情報 入力項目

| 項目名 | 属性名 | バリデーション |
| --- | --- | --- |
| 項目名               | フィールド名                    | バリデーション条件                                                                 |
| ユーザ名             | `name`                          | 入力値.name が未入力 または 50文字以上                                             |
| メールアドレス       | `email`                         | 入力値.email が未入力<br/>smo-module-validator の isValidEmailAddress 関数の返却値が false<br/>入力値.email が128文字以上 |


### 詳細情報1 入力項目

| 項目名       | 属性名               | 型             | 長さ       | バリデーション                                                                 |
|--------------|----------------------|----------------|------------|---------------------------------------------------------------------------------|
| 姓           | `oidc.family_name`   | string         | 2047文字   | 2047文字以内で入力                                                             |
| ミドルネーム | `oidc.middle_name`   | string         | 2047文字   | 2047文字以内で入力                                                             |
| 名           | `oidc.given_name`    | string         | 2047文字   | 2047文字以内で入力                                                             |
| ニックネーム | `oidc.nickname`      | string         | 2047文字   | 2047文字以内で入力                                                             |
| 住所         | `oidc.address`       | string         | 2047文字   | 2047文字以内で入力                                                             |
| 電話番号     | `oidc.phone_number`  | string         | 20文字     | 「＋{国際コード}-{電話番号}」フォーマット、数字のみ可、20文字以内で入力        |
| 生年月日     | `oidc.birthdate`     | string / Date  | -          | `YYYY-MM-DD` フォーマット                                                     |
                                                         

### 詳細情報2 入力項目

| 項目名               | 属性名                     | 型     | 長さ     | バリデーション                       |
|----------------------|----------------------------|--------|----------|--------------------------------------|
| ニックネーム又は表示 | `oidc.preferred_username`  | string | 2047文字 | 2047文字以内で入力                   |
| ウェブサイトURL      | `oidc.website`              | string | 2047文字 | 2047文字以内で入力                   |
| プロフィール画像URL  | `oidc.picture`              | string | 2047文字 | 2047文字以内で入力                   |
| プロフィール情報URL  | `oidc.profile`              | string | 2047文字 | 2047文字以内で入力                   |
| 性別                 | `oidc.gender`               | string | -        | -                                    |
| 言語                 | `oidc.locale`               | string | -        | -                                    |
| タイムゾーン         | `oidc.zoneinfo`             | string | -        | -                                    |
                                                                                

### アクション

| アクション | 処理内容 |
| --- | --- |
|  `変更` ボタンクリック | バリデーション後、API呼び出し |

#### ボタン押下
- 更新確認ダイアログを表示
- API PUT /userpools/self/users でデータを更新する
- 更新後、「更新しました」というトーストを表示

#### フォーム送信　・・・

-  `変更` ボタンクリック


### 状態管理
- useState使用
- オブジェクト：
```ts
type User = {
  name: string;
  email: string;
  groups: string[];
  id: string;
  status?: boolean;
  oidc: Partial<OIDC>;
};

type OIDC = {
  phone_number: string;
  birthdate: string | Date;
  family_name: string;
  middle_name: string;
  given_name: string;
  nickname: string;
  address: string;
  gender: string;
  preferred_username: string;
  zoneinfo: string;
  locale: string;
  website: string;
  picture: string;
  profile: string;
};
```

## 処理方式検討内容（必要な場合）

- 画面マウント時、`更新`ボタンクリック時にAPIからデータ取得

## 新規利用ライブラリ（必要な場合）
- なし

## テスト方針
- ローカルからMock、AWSにデプロイされたAPIいずれかに接続して、テストする


## デザイン/UI
- ガイドラインに準拠する
- 画面イメージ（必要に応じて）
- デザインの参考元（必要に応じて）
