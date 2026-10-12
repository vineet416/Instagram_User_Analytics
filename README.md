# Instagram User Analytics (SQL)

A MySQL analysis of a synthetic Instagram clone database (`ig_clone`). It answers 7 business questions from marketing and investor teams.
The work covers loyal users, inactive users, a photo contest, hashtags, ad timing, engagement and bot detection.

## Project Files

| File | Description |
|------|-------------|
| `ig_clone-Dataset.sql` | Creates the `ig_clone` database, 7 tables and all data inserts |
| `Instagram User Analytics Project.sql` | The analysis queries (Marketing Analysis and Investor Metrics) |
| `Instagram User Analytics (Report).pdf` | 11-page report with each query, a result screenshot and a short conclusion |

## Dataset

100 users, 257 photos, 8,782 likes, 7,488 comments, 7,623 follows, 21 tags, 501 photo-tag links.

| Table | Key fields | Description |
|-------|-----------|-------------|
| `users` | `id`, `username`, `created_at` | Registered accounts |
| `photos` | `id`, `image_url`, `user_id`, `created_dat` | Posted photos (the timestamp column name is a typo) |
| `likes` | `user_id`, `photo_id` | Who liked which photo (composite key) |
| `comments` | `id`, `comment_text`, `user_id`, `photo_id` | Comments on photos |
| `follows` | `follower_id`, `followee_id` | Follower relationships |
| `tags` | `id`, `tag_name` | Hashtag dictionary |
| `photo_tags` | `photo_id`, `tag_id` | Links photos to hashtags |

## Approach

1. **Understand the data:** reviewed the 7-table schema and its primary and foreign keys.
2. **Load:** ran the dataset script in MySQL to build `ig_clone`.
3. **Analyse:** wrote one query per business question using joins, aggregates, `GROUP BY` and subqueries.
4. **Report:** documented each query, result and takeaway in the PDF.
5. **Verify:** every figure below was recomputed from the raw inserts, not copied from the report.

## Key Insights

| Question | Result (recomputed) |
|----------|---------------------|
| Five oldest users | Darby_Herzog (2016-05-06), Emilio_Bernier52, Elenor88, Nicole71, Jordyn.Jacobson2 |
| Users who never posted | **26 of 100** (26%) |
| Contest winner | Zack_Kemmer93 (user 52), photo 145, **48 likes**; runner-up has 43 |
| Top hashtags | smile (59), beach (42), party (39), fun (38); food, lol and concert tie at 24 |
| Best registration day | Thursday and Sunday tie at **16** users each; Friday has 15, Saturday 12 |
| Photos per user | 257 / 100 = **2.57** (3.47 among the 74 users who posted) |
| Possible bots | **13 users** liked all 257 photos; all 13 have posted nothing |

- The 13 bot-like accounts cast 3,341 likes (38% of all likes).
- Without their likes, the contest winner is unchanged (photo 145 drops to 35 likes).
- Weekday registrations range only from 12 to 16, so the day-of-week signal is weak.
- Half of the 26 non-posters (13) are the bot-like accounts, which suggests the real inactive group is smaller.

## Tech Stack

- MySQL 8.0.34 and MySQL Workbench (per the report)
- SQL: `JOIN` (inner, left, right), `GROUP BY`, `HAVING`, subqueries, `DAYNAME()`, `ORDER BY ... LIMIT`

## How to Use

1. Install MySQL and open a client such as MySQL Workbench.
2. Run `ig_clone-Dataset.sql` to create and populate `ig_clone`.
3. Run `Instagram User Analytics Project.sql` (it starts with `use ig_clone;`).
4. Compare the output with the screenshots in the PDF report.
