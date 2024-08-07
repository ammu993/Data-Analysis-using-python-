![banner for readme](https://github.com/user-attachments/assets/b40d78e7-34f3-478b-a544-5d3b4500b926)

# ANALYSIS OF REGIONAL MUSIC PREFERENCES(DEC 2023 - JUN 2024) USING  PYTHON

## Overview
This project analyzes the top Spotify songs in 73 countries over a six-month period from December 1, 2023, to June 1, 2024. The aim is to understand the music preferences of Spotify users across different regions: North America, Latin America, Europe, and the Rest of the World. By examining this dataset, we can identify regional daily trends and top artists that define the global music landscape during this period.

## Project Structure
Following steps were performed on the dataset to gain insights:
+ Data Cleaning:
  * Handled missing values and ensured data consistency.
  * Removed irrelevant columns and filtered data based on the analysis period.
+ Exploratory Data Analysis (EDA):
  * Conducted initial data exploration to understand the basic structure and key features of the dataset.
  * Generated summary statistics and visualizations to identify trends and patterns.
+ Main Analysis:
  * Analyzed music preferences across different regions (North America, Latin America, Europe, and the Rest of the World).
  * Examined trends in the popularity and daily rankings of the top songs globally and regionally.
  * Investigated regional differences in the audio characteristics of the most popular songs.
  * Identified top artists per region and their presence in the daily top ranks.
+ Insights and Recommendations:
  * Provided actionable recommendations to stakeholder groups: 1) Artists & their Record Label 2)Spotify .

## Tools/Libraries

The following libraries were used for data processing, analysis, and visualization:

- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`

## Data Source
The dataset used in this analysis is [Top Spotify Songs in 73 Countries (Daily Updated)](https://www.kaggle.com/datasets/asaniczka/top-spotify-songs-in-73-countries-daily-updated/data) provided by user **asaniczka** on Kaggle. This dataset is licensed under the Open Data Commons Attribution License (ODC-By) v1.0.

## Research Questions
Music Preferences Across Regions:
- What were the music preferences across different regions (North America, Latin America, Europe, and the Rest of the World) on Spotify and how did they vary from December 2023 to June 2024?

Trends in Popularity and Rankings:
- What were the trends in the popularity and daily rankings of the top songs globally?
- How did the daily rankings of the top songs differ across regions?
  
Regional Differences in Audio Characteristics:
- What regional differences can be observed in the audio characteristics of the most popular songs?

Top Artists per Region:
- Who were the top artists per region, and how often do their songs appear in the top daily ranks?

## Data Processing 
For Complete code : [Data_Analysis_Python_Music_Preferences_Spotify_.ipynb](https://github.com/ammu993/Data-Analysis-using-python-/blob/6439b378c5af346f75e13db8e2643311bd0491a2/Data_Analysis_Python_Music_Preferences_Spotify_.ipynb)
Code snippets:
```python
#Function to list top n songs within a region based on their minimum daily rankings
def top_music(df1,region, top_n):
    # Filter the data for the given region
    regional_data = df1[df1['regions'] == region]

    # Grouping the data by song name and snapshot_date
    grouped = regional_data.groupby(['name', 'snapshot_date'])['daily_rank'].min().reset_index()

    # Select the top N songs based on the minimum daily rank
    top_songs = grouped['name'].value_counts().head(top_n).reset_index()
    top_songs_list = top_songs['name'].tolist()
    return top_songs_list
```

Code snippet to visualize trend of popularity score and daily rank 
```python
#Plotting popularity score and daily rank trend of top 5 songs
colors=['#26CC50','#7C71BB' ,'#A8B0BA','#A8B0BA','#A9B0BA']
linestyles = ['-', '-', '-', '--', ':']
plt.style.use('default')

# Figure with two subplots
fig, (ax1,ax2) = plt.subplots(figsize=(16, 10),nrows=2, ncols=1, sharex=True)

# Plotting each song's popularity score trend
for i, song in enumerate(songs_top5):
     song_data = top_songs_2024[top_songs_2024['name'] == song]
     ax1.plot(song_data['snapshot_date'], song_data['popularity'],color=colors[i],linestyle=linestyles[i], label=song)
# Plotting each song's daily ranking trend
for i, song in enumerate(songs_top5):
    song_data = top_songs_2024[top_songs_2024['name'] == song]
    ax2.plot(song_data['snapshot_date'], song_data['daily_rank'],color=colors[i],linestyle=linestyles[i], label=song)

#Popularity trend
ax1.set_xlabel('Date')
ax1.set_ylabel('Popularity Score')
ax1.set_title('Popularity Score Trend for Top 5 Songs(Global)')
ax1.legend(fontsize='medium',loc='lower right')
ax1.grid(axis= 'x',color='grey', linestyle='-', linewidth=0.5, alpha=0.3)
#Daily rankings
ax2.set_xlabel('Date')
ax2.yaxis.set_major_locator(ticker.MaxNLocator(integer=True))
ax2.set_ylabel('Daily rankings')
ax2.set_title('Daily Global Rankings of Top 5 Songs')
ax2.grid(axis= 'x',color='grey', linestyle='-', linewidth=0.5, alpha=0.3)
plt.tight_layout()
```

## Results and Visualisations
![pop score](https://github.com/user-attachments/assets/620958d4-07d2-4758-aaa7-3147bb9bf587)
Daily Rankings vs Popularity Score: Daily rankings provide a better measurement of global music preferences than popularity scores, as songs with a zero popularity score can still be ranked first.

![daily rank of top 5](https://github.com/user-attachments/assets/b917c1c0-8230-43ce-9aaa-6caa675efe94)
Daily Ranking Trends of Top 5 Songs by Region
* Europe:
Top songs that ranked high (1-10) in the winter months moved further down the ranking list after April.
* North America:
Top songs ranked low (>10) in December and between January and mid-April held consistent high rankings.
* Latin America and Rest of the World:
Rankings exhibit significant fluctuations.

![audio features 1](https://github.com/user-attachments/assets/0ee4ed0f-0d95-4955-9887-250b127d7b90)
Music Preferences According to Audio Features
* Danceability:
Highly preferred in all regions, especially in Europe and Latin America.
* Energy Levels:
Fairly similar across all regions, with Europe and Latin America showing slightly higher values.
* Speechiness:
Europe shows a slightly higher value, indicating a preference for tracks with more spoken words.
* Acousticness and Instrumentalness:
Europe shows a higher preference for acoustic and instrumental tracks.
North America and the Rest of the World show a minor preference for live performance elements.
* Valence:
Highest in Latin America, followed by the Rest of the World and Europe, indicating a preference for positive or euphoric songs.

![tempo](https://github.com/user-attachments/assets/9562e4f3-8759-4ffc-8ec5-aa779e6d186d)
Latin America and North America prefer faster-paced music, while Europe favors slower-paced tracks. The Rest of the World falls in between but leans towards faster tempos.

![loudness](https://github.com/user-attachments/assets/8de5c339-3fa3-4571-b5fa-d3d5513a4091)
Latin America prefers the loudest music, followed by North America and then Europe. The Rest of the World prefers the quietest tracks.

![top artists](https://github.com/user-attachments/assets/1362ab1e-0861-4789-aaf1-24b5e3040ffc)
Top Artists per Region

## Conclusion
This project provides a comprehensive analysis of Spotify music preferences across different regions over a six-month period. The insights gained can help understand listener habits, regional differences in music tastes, and the popularity trends of artists and genres.

For further details, analysis and stakeholder specific recommendations, refer to the attached 'Data_Analysis_Python_Music_Preferences_Spotify_.ipynb' file



