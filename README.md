# SQL-Single-Table-Project-on-Spotify-s-Most-Streamed-Songs-2024
This project is to showcase SQL commands performed on single table

>Renamed colomns from original dataset to songs_artist , total_streams, daily_streams for ease of query

1.View entire table.
2.Find out most streamed song globally.
3.Find songs from Ed Sheean with more than 200000 views in last 24 hours from highest to lowest.
4.Total number of songs with daily streams within 100000 to 300000 range.
5.Separating artist name from song name.


>View entire table

```SELECT *
FROM `spotify_artist_data`;```

>Find out most streamed song globally

```SELECT songs_artist, total_streams
FROM spotify_artist_data
WHERE total_streams = 
		(SELECT MAX(total_streams) FROM spotify_artist_data);``` [^Subquery to find highest stream]

>Find songs from Ed Sheean with more than 200000 views in last 24 hours from highest to lowest

```SELECT songs_artist, daily_streams
FROM spotify_artist_data
WHERE songs_artist REGEXP 'ED Sheeran' AND daily_streams >= 200000  [^Regular expression]
ORDER BY daily_streams DESC;```

>Total number of songs with daily streams within 100000 to 300000 range

```SELECT COUNT(songs_artist) as 'Number of Songs' -- alias
FROM spotify_artist_data
WHERE daily_streams BETWEEN 100000 AND 300000;```

>Separating artist name from song name

```SELECT *
FROM (
    SELECT
        SUBSTRING_INDEX(songs_artist, '-', 1) AS artist_name,
        SUBSTRING_INDEX(songs_artist, '-', -1) AS song_name,
        total_streams,
        daily_streams
    FROM spotify_artist_data
) AS artist_data```
