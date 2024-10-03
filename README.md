# SQL-Single-Table-Project-on-Spotify-s-Most-Streamed-Songs-2024
This project is to showcase SQL commands performed on single table

>Renamed colomns from original dataset to songs_artist , total_streams, daily_streams for ease of query

1. View entire table...
2. Find out most streamed song globally...
3. Find songs from Ed Sheean with more than 200000 views in last 24 hours from highest to lowest...
4. Total number of songs with daily streams within 100000 to 300000 range...
5. Separating artist name from song name...


>View entire table

--SELECT *
FROM `spotify_artist_data`;--

![View Entire Table](https://github.com/user-attachments/assets/e025d12b-40ff-4478-bf25-43b85f36301e)

--



>Find out most streamed song globally

--SELECT songs_artist, total_streams
FROM spotify_artist_data
WHERE total_streams = 
		(SELECT MAX(total_streams) FROM spotify_artist_data);--

[^Subquery to find highest stream]

![most streamed song globally](https://github.com/user-attachments/assets/b3438f6c-7c61-400f-a36d-1af08846c635)

--


>Find songs from Ed Sheean with more than 200000 views in last 24 hours from highest to lowest

--SELECT songs_artist, daily_streams
FROM spotify_artist_data
WHERE songs_artist REGEXP 'ED Sheeran' AND daily_streams >= 200000  [^Regular expression]
ORDER BY daily_streams DESC;--

![songs from Ed Sheean with more than 200000 views in last 24 hours from highest to lowest](https://github.com/user-attachments/assets/b2f9acc2-8483-4caa-a88a-b6454aaa9ac3)


>Total number of songs with daily streams within 100000 to 300000 range

--SELECT COUNT(songs_artist) as 'Number of Songs'
FROM spotify_artist_data
WHERE daily_streams BETWEEN 100000 AND 300000;--

![Total number of songs with daily streams within 100000 to 300000 range](https://github.com/user-attachments/assets/85c1b313-023c-44a3-b367-92faf0a9ee2e)


>Separating artist name from song name

--SELECT *
FROM (
    SELECT
        SUBSTRING_INDEX(songs_artist, '-', 1) AS artist_name,
        SUBSTRING_INDEX(songs_artist, '-', -1) AS song_name,
        total_streams,
        daily_streams
    FROM spotify_artist_data
) AS artist_data--

![Separating artist name from song name](https://github.com/user-attachments/assets/717d0ae8-be69-4f0b-8b23-c8c85e20fc8a)


