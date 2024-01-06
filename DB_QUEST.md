# インターネットTV
## 1.テーブル作成

### ユーザーテーブル
| カラム名    | データ型     | NULL | キー    | 初期値 | AUTO INCREMENT |
| ----------- | ------------ | ---- | ------- | ------ | -------------- |
| user_id     | bigint(20)   |      | PRIMARY |        | YES            |
| user_name   | varchar(100) |      |         |        |                |
| email       | varchar(100) | YES  |         |        |                |

### チャンネルテーブル
| カラム名    | データ型     | NULL | キー    | 初期値 | AUTO INCREMENT |
| ----------- | ------------ | ---- | ------- | ------ | -------------- |
| channel_id  | bigint(20)   |      | PRIMARY |        | YES            |
| channel_name| varchar(100) |      |         |        |                |

### プログラムテーブル
| カラム名    | データ型     | NULL | キー    | 初期値 | AUTO INCREMENT |
| ----------- | ------------ | ---- | ------- | ------ | -------------- |
| program_id  | bigint(20)   |      | PRIMARY |        | YES            |
| title       | varchar(100) |      |         |        |                |
| summary     | text         | YES  |         |        |                |

### エピソードテーブル
| カラム名          | データ型     | NULL | キー    | 初期値 | AUTO INCREMENT |
| ----------------- | ------------ | ---- | ------- | ------ | -------------- |
| episode_id        | bigint(20)   |      | PRIMARY |        | YES            |
| program_id        | bigint(10)   |      | FOREIGN |        |                |
| episode_title     | varchar(100) |      |         |        |                |
| episode_summary   | text         | YES  |         |        |                |
| season_no         | int          | YES  |         |        |                |
| episode_no        | int          | YES  |         |        |                |

### タイムテーブル
| カラム名        | データ型   | NULL | キー    | 初期値 | AUTO INCREMENT |
| --------------- | ---------- | ---- | ------- | ------ | -------------- |
| time_id         | bigint(20) |      | PRIMARY |        | YES            |
| channel_id      | bigint(20) |      | FOREIGN |        |                |
| episode_id      | bigint(20) |      | FOREIGN |        |                |
| start_time      | datetime   |      |         |        |                |
| end_time        | datetime   |      |         |        |                |
| view_count      | int(10)    |      |         |        |                |

### ジャンルテーブル
| カラム名        | データ型     | NULL | キー    | 初期値 | AUTO INCREMENT |
| -----------     | ------------ | ---- | ------- | ------ | -------------- |
| category_id     | bigint(20)   |      | PRIMARY |        | YES            |
| category_name   | varchar(100) |      |         |        |                |

### プログラムジャンルテーブル
| カラム名            | データ型   | NULL | キー    | 初期値 | AUTO INCREMENT |
| ----------          | ---------- | ---- | ------- | ------ | -------------- |
| program_category_id | bigint(20) |      | PRIMARY |        | YES            |
| program_id          | bigint(20) |      | FOREIGN |        |                |
| category_id         | bigint(20) |      | FOREIGN |        |                |

## ２.テーブル作成

### テーブル作成
```sql:テーブル作成
#データベース作成
create database quest
use quest

#ユーザテーブル
create table user 
(user_id bigint(20) not null auto_increment primary key,
user_name varchar(100) not null,
email varchar(100) not null unique key);

#チャンネルテーブル
create table channel 
(channel_id bigint(20) not null auto_increment primary key,
channel_name varchar(100) not null );

#プログラムテーブル
create table program 
(program_id bigint(20) not null auto_increment primary key,
title varchar(100) not null,
summary text);

#エピソードテーブル
create table episode 
(episode_id bigint(20) not null auto_increment primary key,
program_id bigint(20) not null,
episode_title varchar(100) not null,
episode_summary text , 
season_no int ,
episode_no int , 
foreign key (program_id) references program (program_id));

＃タイムテーブル
create table time_table
( time_id bigint(20) not null auto_increment primary key,
channel_id bigint(20) not null,
episode_id bigint(20) not null,
start_time datetime not null,
end_time datetime not null,
view_count int(10) not null default 0,
foreign key (channel_id) references channel (channel_id),
foreign key (episode_id) references episode (episode_id));

#ジャンルテーブル
create table category 
(category_id bigint(20) not null auto_increment primary key,
category_name varchar(100) not null );

#プログラムジャンルテーブル
create table program_category
(program_category_id bigint(20) not null auto_increment primary key,
program_id bigint(20) not null,
category_id bigint(20) not null,
foreign key (program_id) references program (program_id),
foreign key (category_id) references category (category_id) );
```
### サンプルデータ生成
```sql:サンプルデータ
#ユーザーサンプル
INSERT INTO user (user_name, email)
VALUES
('John Doe', 'john.doe@example.com'),
('Alice Smith', 'alice.smith@example.com'),
('Bob Johnson', 'bob.johnson@example.com'),
('Eva Williams', 'eva.williams@example.com'),
('Michael Brown', 'michael.brown@example.com'),
('Sophia Davis', 'sophia.davis@example.com'),
('Daniel Miller', 'daniel.miller@example.com'),
('Olivia Garcia', 'olivia.garcia@example.com'),
('William Rodriguez', 'william.rodriguez@example.com'),
('Emma Martinez', 'emma.martinez@example.com');

#チャンネルサンプル
INSERT INTO channel (channel_name)
VALUES
("Anime"),
("Variety"),
("Drama"),
("Mahjong"),
("Sports"),
("News"),
("Pets");

#カテゴリーテーブル
INSERT INTO category (category_name)
VALUES
("Anime"),
("Variety"),
("Drama"),
("Mahjong"),
("Sports"),
("News"),
("Pets");

insert into program (title, summary) VALUES
("Sazae-san", "A nationally beloved anime depicting everyday life."),
("Crayon Shin-chan", "An anime that combines humor and touching moments."),
("Sex and the City", "A TV series following the lives and romantic escapades of four women living in New York City."),
("The Walking Dead", "A TV series depicting the struggles of a group of survivors in a zombie-infested post-apocalyptic world."),
("World Athletics Championships", "Live coverage of the world's top athletic event."),
("CNN", "A news channel providing global coverage of current events."),
("Discovery Channel", "An educational and documentary channel featuring a variety of topics."),
("Superman", "An animated series portraying the adventures of Superman."),
("Spider-Man", "An animated series depicting the superhero exploits of Spider-Man."),
("Prison Break", "A thrilling TV series centered around a man determined to prove his brother's innocence by orchestrating an elaborate prison break."),
("Mahjong Championship", "Fierce competition among professional mahjong players."),
("The Ellen DeGeneres Show", "A popular daytime talk show hosted by Ellen DeGeneres, featuring celebrity interviews, musical performances, and comedic segments.");

insert into program_category (program_id, category_id) VALUES 
(1,1),
(2,1),
(3,3),
(4,3),
(5,5),
(6,6),
(7,7),
(8,1),
(9,1),
(10,3),
(11,4),
(12,2);

insert into episode (program_id, episode_title, episode_summary, episode_no, season_no) VALUES
(1,"Sazae-san Episode 1", "Masuo's Holiday", 1,1),
(1,"Sazae-san Episode 2", "Tamao's Holiday", 2,1),
(1,"Sazae-san Episode 3", "Katsuo's Holiday", 3,1),
(1,"Sazae-san Episode 4", "Wakame's Holiday", 4,1),
(1,"Sazae-san Episode 5", "Sazae's Holiday", 5,1),
(1,"Sazae-san 2 Episode 1", "Masuo's Weekday", 1,2),
(1,"Sazae-san 2 Episode 2", "Tamao's Weekday", 2,2),
(1,"Sazae-san 2 Episode 3", "Katsuo's Weekday", 3,2),
(2,"Crayon Shin-chan Episode 1", "Shin's Day", 1,1),
(2,"Crayon Shin-chan Episode 1", "Shin's Day 2", 1,2),
(2,"Crayon Shin-chan 2 Episode 1", "Shin's Day 3", 2,1),
(2,"Crayon Shin-chan 2 Episode 1", "Shin's Day 4", 2,2),
(3, "Sex and the City Episode 1", "Search for True Love", 1, 1),
(3, "Sex and the City Episode 2", "Dating in the City", 2, 1),
(3, "Sex and the City Episode 3", "Fashion Frenzy", 3, 1),
(3, "Sex and the City Episode 4", "Friendship Dilemmas", 4, 1),
(4, "Prison Break Episode 1", "Escape Plan", 1, 1),
(4, "Prison Break Episode 2", "Infiltrating the Prison", 2, 1),
(4, "Prison Break Season2 Episode 1", "The Brotherhood", 1, 2),
(4, "Prison Break Season2 Episode 2", "On the Run", 2, 2),
(5, "World Athletics Championships", "Men's 100m Sprint", null, null),
(6, "CNN", "Breaking News", null, null),
(7, "Discovery Channel", "Nature's Wonders", null, null),
(8, "Superman", null, null, null),
(9, "Spider-Man", null, null, null),
(10, "The Walking Dead", null, null, null),
(11, "Mahjong Championship", null, null, null),
(12, "The Ellen DeGeneres Show", null, null, null);

INSERT INTO time_table (channel_id, episode_id, start_time, end_time, view_count)
VALUES
  (1, 1, '2024-01-01 08:00:00', '2024-01-01 08:30:00', 5432),
  (1, 2, '2024-01-02 09:15:00', '2024-01-02 09:45:00', 7891),
  (1, 3, '2024-01-03 12:30:00', '2024-01-03 13:00:00', 2345),
  (1, 4, '2024-01-04 14:45:00', '2024-01-04 15:15:00', 4567),
  (1, 5, '2024-01-05 18:00:00', '2024-01-05 18:30:00', 3123),
  (1, 6, '2024-01-06 20:00:00', '2024-01-06 20:30:00', 6542),
  (1, 7, '2024-01-07 08:00:00', '2024-01-07 08:30:00', 1987),
  (1, 8, '2024-01-08 09:15:00', '2024-01-08 09:45:00', 4321),
  (1, 9, '2024-01-09 12:30:00', '2024-01-09 13:00:00', 5678),
  (1, 10, '2024-01-10 14:45:00', '2024-01-10 15:15:00', 7890),
  (1, 11, '2024-01-11 18:00:00', '2024-01-11 18:30:00', 2345),
  (1, 12, '2024-01-12 20:00:00', '2024-01-12 20:30:00', 6543),
  (2, 13, '2024-01-13 08:00:00', '2024-01-13 08:30:00', 5532),
  (2, 14, '2024-01-14 09:15:00', '2024-01-14 09:45:00', 7791),
  (2, 15, '2024-01-15 12:30:00', '2024-01-15 13:00:00', 2445),
  (2, 16, '2024-01-16 14:45:00', '2024-01-16 15:15:00', 4767),
  (2, 17, '2024-01-17 18:00:00', '2024-01-17 18:30:00', 3723),
  (2, 18, '2024-01-18 20:00:00', '2024-01-18 20:30:00', 6242),
  (2, 19, '2024-01-19 08:00:00', '2024-01-19 08:30:00', 1487),
  (2, 20, '2024-01-20 09:15:00', '2024-01-20 09:45:00', 4121),
  (3, 21, '2024-01-21 12:30:00', '2024-01-21 13:00:00', 5478),
  (4, 22, '2024-01-22 14:45:00', '2024-01-22 15:15:00', 7990),
  (7, 23, '2024-01-23 18:00:00', '2024-01-23 18:30:00', 2445),
  (1, 24, '2024-01-24 20:00:00', '2024-01-24 20:30:00', 5147),
  (1, 25, '2024-01-25 20:00:00', '2024-01-25 20:30:00', 2221),
  (3, 26, '2024-01-26 20:00:00', '2024-01-26 20:30:00', 3665),
  (4, 27, '2024-01-27 20:00:00', '2024-01-27 20:30:00', 5555),
  (2, 28, '2024-01-28 20:00:00', '2024-01-28 20:30:00', 7744);
```
## 3.データ抽出クエリ
### 1.よく見られているエピソードを知りたいです。エピソード視聴数トップ3のエピソードタイトルと視聴数を取得してください
```sql:入力コード1
select e.episode_title, t.view_count
from program as p
inner join episode as e on p.program_id = e.program_id
inner join time_table as t on e.episode_id = t.episode_id
order by t.view_count desc
limit 3;
```
```sql:出力結果2
+----------------------------+------------+
| episode_title              | view_count |
+----------------------------+------------+
| CNN                        |       7990 |
| Sazae-san Episode 2        |       7891 |
| Crayon Shin-chan Episode 1 |       7890 |
+----------------------------+------------+
```
### 2. よく見られているエピソードの番組情報やシーズン情報も合わせて知りたいです。エピソード視聴数トップ3の番組タイトル、シーズン数、エピソード数、エピソードタイトル、視聴数を取得してください
```sql:入力コード2
select p.title, e.season_no, e.episode_no, e.episode_title, t.view_count
from program as p
inner join episode as e on p.program_id = e.program_id
inner join time_table as t on e.episode_id = t.episode_id
order by t.view_count desc
limit 3;
```
```sql:出力結果2
+------------------+-----------+------------+----------------------------+------------+
| title            | season_no | episode_no | episode_title              | view_count |
+------------------+-----------+------------+----------------------------+------------+
| CNN              |      NULL |       NULL | CNN                        |       7990 |
| Sazae-san        |         1 |          2 | Sazae-san Episode 2        |       7891 |
| Crayon Shin-chan |         2 |          1 | Crayon Shin-chan Episode 1 |       7890 |
+------------------+-----------+------------+----------------------------+------------+
```

### 3. 本日の番組表を表示するために、本日、どのチャンネルの、何時から、何の番組が放送されるのかを知りたいです。本日放送される全ての番組に対して、チャンネル名、放送開始時刻(日付+時間)、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を取得してください。なお、番組の開始時刻が本日のものを本日放送される番組とみなすものとします
```sql:入力コード3
select c.channel_name, t.start_time, t.end_time, e.season_no, e.episode_no, e.episode_title, e.episode_summary
from channel as c
inner join time_table as t on c.channel_id = t.channel_id
inner join episode as e on t.episode_id = e.episode_id
where t.start_time >= timestamp('2024-01-06 00:00:00')
and t.start_time < timestamp('2024-01-07 00:00:00')
order by c.channel_id asc, t.start_time asc;
```
```sql:出力結果3
+--------------+---------------------+---------------------+-----------+------------+-----------------------+-----------------+
| channel_name | start_time          | end_time            | season_no | episode_no | episode_title         | episode_summary |
+--------------+---------------------+---------------------+-----------+------------+-----------------------+-----------------+
| Anime        | 2024-01-06 20:00:00 | 2024-01-06 20:30:00 |         2 |          1 | Sazae-san 2 Episode 1 | Masuo's Weekday |
+--------------+---------------------+---------------------+-----------+------------+-----------------------+-----------------+
```

### 4.ドラマというチャンネルがあったとして、ドラマのチャンネルの番組表を表示するために、本日から一週間分、何日の何時から何の番組が放送されるのかを知りたいです。ドラマのチャンネルに対して、放送開始時刻、放送終了時刻、シーズン数、エピソード数、エピソードタイトル、エピソード詳細を本日から一週間分取得してください
```sql:入力コード4
select c.channel_name, t.start_time, t.end_time, e.season_no, e.episode_no , e.episode_title, e.episode_summary
from episode as e
inner join time_table as t on e.episode_id = t.episode_id
inner join channel as c on t.channel_id = c.channel_id
where channel_name = 'Drama'
and t.start_time >= timestamp('2024-01-01 00:00:00')
and t.start_time < timestamp('2024-01-08 00:00:00')
order by t.start_time asc;
```

```sql:出力結果
Empty set (0.01 sec)
```
