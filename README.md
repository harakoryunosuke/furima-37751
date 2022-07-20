# テーブル設計

## users テーブル

| Column           | Type   | Options     |
| ---------------- | ------ | ----------- |
| nickname         | string | null: false |
| email            | string | null: false |
| encrypted        | string | null: false |
| user_image       | string |             |
| introduction     | text   |             |
| family_name      | string | null: false |
| first_name       | string | null: false |
| family_name_kana | string | null: false |
| first_name_kana  | string | null: false |
| birth_day        | date   | null: false |

### Association

- has_many :items dependent: :destroy
- belongs_to :destination dependent: :destroy
- belongs_to :card dependent: :destroy

## destination テーブル

| Column           | Type    | Options                        |
| ---------------- | ------- | ------------------------------ |
| user_id          | integer | null: false, foreign_key: true |
| family_name      | string  | null: false                    |
| first_name       | string  | null: false                    |
| family_name_kana | string  | null: false                    |
| first_name_kana  | string  | null: false                    |
| post_code        | string  | null: false                    |
| prefecture       | string  | null: false                    |
| city             | string  | null: false                    |
| address          | string  | null: false                    |
| building_name    | string  |                                |
| phone_number     | string  |                                |

### Association

- belongs_to :user

## card テーブル

| Column      | Type    | Options                        |
| ----------- | ------- | ------------------------------ |
| user_id     | integer | null: false, foreign_key: true |
| customer_id | string  | null: false                    |
| card_id     | string  | null: false                    |

### Association

- belongs_to :user

## category テーブル

| Column   | Type   | Options     |
| -------- | ------ | ----------- |
| name     | string | null: false |
| ancestry | string |             |

### Association

- has_many :items

## items テーブル

| Column        | Type    | Options                        |
| ------------- | ------- | ------------------------------ |
| name          | string  | null: false                    |
| price         | string  | null: false                    |
| description   | string  | null: false                    |
| status        | string  | null: false                    |
| size          | string  | null: false                    |
| shipping_cost | string  | null: false                    |
| shipping_days | string  | null: false                    |
| prefecture_id | string  | null: false                    |
| judgment      | string  |                                |
| category_id   | integer | null: false, foreign_key: true |
| brand_id      | integer | null: false, foreign_key: true |
| shipping_id   | integer | null: false, foreign_key: true |
| user_id       | integer | null: false, foreign_key: true |

### Association

- belongs_to :user dependent: :destroy
- belongs_to :category dependent: :destroy
- belongs_to :brand dependent: :destroy
- has_many :images dependent: :destroy
- belongs_to_active_hash :prefecture

## images テーブル

| Column      | Type    | Options                        |
| ----------- | ------- | ------------------------------ |
| image       | string  | null: false                    |
| item_id     | integer | null: false, foreign_key: true |
| purchase_id | integer | null: false, foreign_key: true |

### Association

- belongs_to :item

## brand テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | index: true |

### Association

- has_many :items