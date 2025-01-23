# Spotify ETL Project

This repository contains a test ETL (Extract, Transform, Load) pipeline for processing data from Spotify playlists. The pipeline extracts playlist data using Spotify's Web API, transforms it into structured datasets, and loads the data into an AWS S3 bucket for further analysis.

## Summary
The project is designed to automate the ingestion and transformation of Spotify playlist data. The pipeline consists of two main stages:

1. **Data Extraction and Storage:** Playlist data is retrieved using the Spotify Web API and stored as raw JSON files in an S3 bucket.
2. **Data Transformation and Loading:** The raw data is processed to extract information about albums, artists, and songs. The transformed data is then saved as CSV files in an S3 bucket for downstream analytics.


## Features
- Extract Spotify playlist data using the Spotipy library.
- Store raw playlist data in an AWS S3 bucket.
- Process raw JSON data to generate clean datasets for albums, artists, and songs.
- Save transformed datasets as CSV files in S3.
- Organize raw data into processed and unprocessed directories within S3.


## Tools and Libraries Used

### Python Libraries:
- **json:** For handling JSON data.
- **os:** To manage environment variables.
- **boto3:** To interact with AWS S3.
- **spotipy:** For accessing the Spotify Web API.
- **pandas:** For data manipulation and transformation.
- **datetime:** For timestamping files.
- **StringIO:** For in-memory file handling.

### AWS Services:
- **S3:** Used for storing raw and transformed data.
- **Lambda:** For deploying and running the ETL pipeline.


## Step-by-Step Overview

### 1. Data Extraction
The pipeline starts by extracting Spotify playlist data using the Spotipy library. The `SpotifyClientCredentials` class handles authentication with the Spotify API using client credentials stored in environment variables. Extracted playlist data is retrieved and saved as raw JSON files in the S3 bucket under the `raw_data/to_process/` directory.

### 2. Data Transformation
Three functions handle the transformation of raw JSON data:

- **`album(data):`** Extracts album-related information such as album ID, name, release date, total tracks, and Spotify URL.
- **`artist(data):`** Extracts artist information including artist ID, name, and external URL.
- **`song(data):`** Extracts song details such as song ID, name, duration, popularity, and associated album and artist IDs.

Each dataset is processed using pandas to ensure clean and deduplicated records.

### 3. Data Loading
The transformed data is saved as CSV files into the following directories within the S3 bucket:
- `transformed_data/album_data/`
- `transformed_data/artist_data/`
- `transformed_data/song_data/`

### 4. Data Organization
Once the raw data is processed, the files are moved from the `raw_data/to_process/` directory to the `raw_data/processed/` directory. The processed files are removed from the `to_process` folder to avoid redundant processing.


## Directory Structure
The S3 bucket is organized as follows:
```
spotify-etl-project-tb
├── raw_data
│   ├── to_process
│   └── processed
├── transformed_data
│   ├── album_data
│   ├── artist_data
│   └── song_data
```


## How to Use

### Prerequisites
- AWS credentials with access to S3.
- Spotify API client credentials (client ID and client secret).
- Python environment with required libraries installed.

### Deployment
1. Set up environment variables for the Spotify API credentials:
   ```bash
   export client_id="your_spotify_client_id"
   export client_secret="your_spotify_client_secret"
   ```

2. Deploy the code to AWS Lambda (or run it locally for testing).

3. Ensure the required S3 bucket structure is created before running the pipeline.


## Further improvement opportunities
- Add more datasets to the analyses
- Create dashboards based on the dataset


## Credits
Special thanks to **Darshil Parmar**, an awesome instructor, for providing guidance and inspiration for this project.


## Summary
This ETL pipeline automates the extraction, transformation, and loading of Spotify playlist data. It leverages Spotify's Web API, AWS S3, and Python libraries for efficient processing. The structured datasets it generates can be used for downstream analysis or reporting. This project demonstrates how to build scalable ETL pipelines using modern tools and cloud services.

Feel free to explore and customize the pipeline for your own use cases!


