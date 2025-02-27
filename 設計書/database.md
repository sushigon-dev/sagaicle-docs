## エンティティの洗い出し

- ユーザー `Users`
  - ユーザー登録、ログイン、プロフィール取得で利用
- ルート `Routes`
  - タイトル、説明、距離、時間、画像、地図 URI、チェックポイント数、更新日時などを保持
- チェックポイント `Checkpoints`
  - 各ルートに含まれる位置情報（名前、緯度、経度）
- タグ `Tags`
  - ルートに紐づくキーワード。API の GetTags で一覧取得
- ルートとタグの関係 `Route_Tags`
  - ルートとタグは多対多の関係になるため、中間テーブルで管理
- いいね `Likes`
  - ユーザーがルートに対して「いいね」をする。ユーザーとルートの多対多の関係
- チェックポイント訪問 `Checkpoint_Visits`
  - 各ユーザーがどのチェックポイントに訪れたかを記録する

## テーブル設計

### `Users` テーブル

- `user_id`: UUID (主キー)
- `user_name`: ユニークなユーザー名
- `password_hash`: パスワードのハッシュ値
- その他、`mileage` や `total_distance` などのユーザー固有情報

### `Routes` テーブル

- `route_id`: UUID (主キー)
- `title`, `description`, `full_description`
- `distance`: 浮動小数点数
- `time`: 整数（所要時間）
- `total_checkpoints`: チェックポイント数
- `map`: 地図の URI
- `update_at`: 更新日（YYYY/MM/DD 形式）
- `created_by`: 作成者のユーザー ID（必要なら外部キー）

### `Route_Images` テーブル

- `id`: 自動採番 ID
- `route_id`: 外部キー (`Routes.route_id`)
- `image_uri`: 画像の URI
- ルート毎に 1 ～ 6 枚の画像が存在するため、専用テーブルにしても良い

### `Tags` テーブル

- `tag_name`: 主キー（例：短い文字列）
- 単純なタグ一覧として管理

### `Route_Tags` テーブル

- `route_id`: 外部キー (`Routes.route_id`)
- `tag_name`: 外部キー (`Tags.tag_name`)
- 複合主キー (`route_id`, `tag_name`)

### `Checkpoints` テーブル

- `id`: 自動採番または複合主キー（`route_id` と `checkpoint_index` の組み合わせ）
- `route_id`: 外部キー (`Routes.route_id`)
- `checkpoint_index`: 各ルート内での順序番号
- `name`, `lat`, `lng`

### `Likes` テーブル

- `route_id`: 外部キー (`Routes.route_id`)
- `user_id`: 外部キー (`Users.user_id`)
- 複合主キー (`route_id`, `user_id`)

### `Checkpoint_Visits` テーブル

- `route_id`: 外部キー (`Routes.route_id`)
- `user_id`: 外部キー (`Users.user_id`)
- `checkpoint_index`: チェックポイント番号（Routes 内でのインデックス）
- 複合主キー (`route_id`, `user_id`, `checkpoint_index`)
- （訪問日時などの追加情報があれば記録）
