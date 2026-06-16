# YouTube Metadata CSV

This repository contains a folder named `new_folder` that holds a CSV file containing YouTube video metadata. The file includes important information about 600 YouTube videos, including video ID, title, description, channel title, publish date, view count, like count, and category.

## Files in this Folder

- `metadata.csv`: This CSV file contains metadata for 600 YouTube videos. The data is structured in 8 columns and includes key information to analyze video performance, categorization, and more.

## 📊 Dataset Schema

The pipeline trains and evaluates on a curated metadata footprint containing 600 distinct samples across balanced safety categories. Below is the technical specification of the underlying schema:

| Column Name | Data Type | Completeness | Description |
| :--- | :--- | :--- | :--- |
| **`video_id`** | String (`object`) | 100% | The unique alphanumeric identifier assigned by YouTube to isolate individual assets. |
| **`title`** | String (`object`) | 100% | The original, raw text of the video title as fetched from the YouTube Data API. |
| **`description`** | String (`object`) | 88.3% | The original raw body text from the video description box (contains null values for empty entries). |
| **`channel_title`** | String (`object`) | 100% | The name/handle of the content creator or channel responsible for the upload. |
| **`publish_date`** | ISO Timestamp (`object`)| 100% | The exact UTC timestamp indicating when the video asset was made public. |
| **`view_count`** | Integer (`int64`) | 100% | Total cumulative view metrics recorded at the moment of ingestion. |
| **`like_count`** | Integer (`int64`) | 100% | Total cumulative user likes associated with the video record. |
| **`category`** | String (`object`) | 100% | The textual label indicating the specific domain class (e.g., *education*, *news*, *accidents*). |
| **`processed_title`** | String (`object`) | 100% | Cleaned version of the title text (lowercased, punctuation stripped, and tokenized for feature extraction). |
| **`processed_description`**| String (`object`) | 88.0% | Cleaned version of the description text body, optimized for vectorization by filtering noise and stop words. |
| **`combined_text`** | String (`object`) | 100% | A merged corpus concatenating `processed_title` and `processed_description` to form a dense semantic block for TF-IDF parsing. |
| **`category_label`** | Integer (`int64`) | 100% | The encoded target value mapping directly to the safety hierarchy model (**0: Safe**, **1: Neutral**, **2: Harmful**). |

## How to Use the CSV File

1. **Download the CSV File**:
   - To download the file, click on `metadata.csv` in the folder and select `Download`.

2. **Load the Data in Python**:
   You can load the CSV file into a pandas DataFrame in Python for further analysis or processing. Here's an example code:

   ```python
   import pandas as pd
   
   # Load the YouTube metadata CSV file
   data = pd.read_csv(FILE_PATH) # Replace FILE_PATH with the path of the file (depending on where you are storing it)
   
   # Display the first few rows of the data
   print(data.head())
