## タグテーブル

- `tags`: 文字列の配列、タグの配列を格納

## ルートテーブル

- `id`: string (UUIDv4) ルートの ID
- `title`: string タイトル
- `description`: string ひとこと説明
- `full_description`: string 説明詳細
- `distance`: float 距離
- `time`: int 目安時間
- `tags`: string[] タグ
- `likes`: int いいね数
- `image`: string 画像の URL (詳細の 0 番目)
- `update_at`: string 更新日 `yyyy/mm/dd`
- `total_checkpoints`: int チェックポイントの要素数
- `images`: string[] 画像の URL
- `map`: string マップの URL

## チェックポイントテーブル

- `name`: string チェックポイントの名前
- `lat`: float 緯度
- `lng`: float 経度

## ユーザーテーブル

- `user_id`: string (UUIDv4) ユーザーの ID
- `user_name`: string ユーザー名
- `hashed_password`:string ハッシュ化したパスワード
- `mileage`: float ユーザーが走行済みの距離
- `total_distance`: float 走行可能距離の最大値

## 中間テーブル

- いいねテーブル (ユーザーとルートの関連): ユーザーがいいねしたルートを記録
- バッジテーブル (ユーザーとルートの関連): ユーザーが取得したバッジのルートを記録
- 訪問済みチェックポイントテーブル (ユーザーとチェックポイントの関連): ユーザーが訪問したチェックポイントを記録

## その他

- `error`: string エラーメッセージ (必須、成功時は空文字列)
