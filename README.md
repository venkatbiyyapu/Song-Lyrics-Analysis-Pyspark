# TF-IDF Song Analysis in Databricks(Pyspark)

## Overview
This project implements a TF-IDF (Term Frequency-Inverse Document Frequency) analysis of song lyrics using PySpark within the Databricks environment. The analysis computes the TF-IDF scores for tokens in a collection of song lyrics, identifies the token with the highest TF-IDF score for each song, and ranks songs based on specified keywords associated with a "sad" mood.

## Objectives
1. Compute the TF-IDF values for each token in a set of song lyrics stored in a Spark DataFrame.
2. Identify the word with the highest TF-IDF score for each song.
3. Rank songs based on the presence of keywords related to a "sad" mood and display the top three songs.

## Requirements
- **Databricks Account**: Access to a Databricks workspace.
- **Apache Spark**: Databricks provides a Spark environment by default.
- **Python 3.x**: The code is implemented in Python.

## Project Structure
- `tf_idf_song_analysis.ipynb`: Jupyter Notebook containing the implementation of the TF-IDF analysis.
- `Songs/`: Directory containing the song lyrics files.
- `README.md`: This README file.

## Getting Started

### Setup
1. **Access Databricks**:
   - Log into your Databricks account and create a new workspace or use an existing one.

2. **Upload Data**:
   - Upload the 15 song lyrics text files to the following directory in Databricks:
     - **Path**: `/FileStore/tables/Songs/`
   - You can do this by navigating to the **Data** tab in Databricks, selecting **Upload**, and choosing the files from your local machine.

3. **Create a Notebook**:
   - Create a new notebook in your Databricks workspace and set the language to Python.

### Running the Code
1. Open the `tf_idf_song_analysis.ipynb` notebook in your Databricks environment.
2. Ensure that the notebook is set to run on a cluster with Spark enabled.
3. Execute the following code cell to read the song files:
   ```python
   songs_rdd = spark.sparkContext.wholeTextFiles("/FileStore/tables/Songs/*").cache()
   ```
4. Continue to execute the cells sequentially to perform the TF-IDF computation and song ranking process.

### Code Implementation
The code performs the following steps:
- Loads the lyrics from the uploaded text files and removes punctuation.
- Computes the Term Frequency (TF) for each token in each song.
- Calculates the Inverse Document Frequency (IDF) for each token based on the total number of documents.
- Computes the TF-IDF score using the formula:

$$
\text{TF-IDF}(w) = \text{TF} \times \log \left( \frac{\text{Total Number of Documents}}{\text{Number of Documents Containing Word } w} \right)
$$

- Creates a DataFrame to store the computed TF, IDF, and TF-IDF values.
- Uses Spark SQL commands to find the highest TF-IDF token for each song.
- Ranks the songs based on their TF-IDF scores for the keywords "tear," "feel," and "hate," and identifies the top three songs.

### Example Output
The output will include:
- A table of TF-IDF scores for each song and token.
- The token with the highest TF-IDF score for each song.
- The top three songs categorized as having a "sad" mood, along with their rank scores.
