## タグテーブル

- `tags`: 文字列の配列、タグの配列を格納
  - 要素数上限: 20
  - 要素１つについて上限: 10 文字、下限: 1 文字

## ルートテーブル

- `id`: string (UUIDv4) ルートの ID
- `title`: string タイトル
  - 上限: 20 文字、下限: 1 文字
- `description`: string ひとこと説明
  - 上限: 60 文字、下限: 1 文字
- `full_description`: string 説明詳細
  - 上限: 200 文字、下限: 1 文字
- `distance`: float 距離
  - 64bit、上限: 符号付き浮動小数 64bit の上限、下限: 0.0
- `time`: int 目安時間
  - 64bit、上限: 符号付き 64bit 整数の上限、下限: 0
- `tags`: string[] タグ
  - 要素数上限: 20、下限: 1
  - 要素１つについて上限: 10 文字、下限: 1 文字
- `likes`: int いいね数
- `image`: string 画像の URL (詳細の 0 番目)
- `update_at`: string 更新日 `yyyy/mm/dd`
- `total_checkpoints`: int チェックポイントの要素数
  - 上限: 20, 下限: 1
- `images`: string[] 画像の URL
  - 要素数上限: 6、下限: 1
  - 要素１つについて上限: 1023 文字、下限: 8 文字
  - URL スキーム: `https://`
  - ドメイン: `github.com/sushigon-dev/sagaicle-docs`, `x162-43-27-150.static.xvps.ne.jp/sushigon-dev/sagaicle-docs`, `153.125.129.128/sushigon-dev/sagaicle-docs` など
  - フォーマット例: `https://example.com/images/{UUIDv4}.{png|jpg|jpeg|webp}`
- `map`: string マップの URL
  - 上限: 1023 文字、下限: 8 文字
  - URL スキーム: `https://`
  - ドメイン: `www.google.com`
  - フォーマット例: `https://www.google.com/maps/embed?pb=めちゃ長い値`

## チェックポイントテーブル

- `name`: string チェックポイントの名前
- `lat`: float 緯度
- `lng`: float 経度

## ユーザーテーブル

- `user_id`: string (UUIDv4) ユーザーの ID
- `user_name`: string ユーザー名
  - 上限: 32 文字、下限: 1 文字
- `hashed_password`:string ハッシュ化したパスワード
  - ハッシュ関数に依存
- `mileage`: float ユーザーが走行済みの距離
  - 64bit
- `total_distance`: float 走行可能距離の最大値
  - 64bit

## 中間テーブル

- いいねテーブル (ユーザーとルートの関連): ユーザーがいいねしたルートを記録
- バッジテーブル (ユーザーとルートの関連): ユーザーが取得したバッジのルートを記録
- 訪問済みチェックポイントテーブル (ユーザーとチェックポイントの関連): ユーザーが訪問したチェックポイントを記録

## その他

- `error`: string エラーメッセージ (必須、成功時は空文字列)
