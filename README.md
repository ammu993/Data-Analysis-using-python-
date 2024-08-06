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


