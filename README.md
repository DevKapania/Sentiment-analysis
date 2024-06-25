Part 1: Extracting and Preparing Comments

Fetching Comments:
We use the YouTube Data API to retrieve comments from a specific video.
Comments are extracted iteratively, handling pagination for large datasets.
Each comment's text, author, and date are stored in a list.
Creating a DataFrame:
The gathered comments are converted into a pandas DataFrame for easy manipulation.
This DataFrame is saved as a CSV file for later use.
Part 2: Processing Comments with Spark

Spark Session & Data Loading:
A Spark session is initialized to handle distributed data processing.
The comment data (CSV file) is loaded into a Spark DataFrame.
The schema of the DataFrame is inspected to understand the data structure.
Data Cleaning:
A custom function (clean_comment) is implemented to:
Remove HTML tags
Decode special characters (entities)
This function is applied, creating a new column with cleaned comments.
Tokenization and Stop Word Removal:
Spark's MLlib library is used for text processing:
Words are extracted from comments using a Tokenizer.
Common stop words (e.g., "the", "a") are removed using StopWordsRemover.
These steps create columns with tokenized words and filtered words.
Deduplication:
Unique comments are obtained by joining filtered words into a single string and then removing duplicates.
Saving Processed Data:
The processed data (including original comments, cleaned comments, filtered words, author details, and timestamps) is saved to a new CSV file.
Existing output directories are cleared to avoid conflicts.
Record Count Monitoring:
The script tracks the number of comments at each stage (initial load, after cleaning, tokenization, etc.) to:
Validate data integrity
Track the effectiveness of data transformations
This pipeline ensures clean and well-structured data, ready for further analysis.

Part 3: Sentiment Analysis with Spark and NLTK

Loading Processed Comments:
The previously processed comment data (CSV) is loaded into a Spark DataFrame.
The schema and sample rows are examined to verify data structure.
Sentiment Analysis UDF:
NLTK's VADER library is used for sentiment analysis.
A user-defined function (analyze_sentiment) is created to apply VADER to each comment.
This function classifies comments as positive, negative, or neutral based on their sentiment score.
A new column named "sentiment" is added to the DataFrame with the sentiment classification.
Sentiment Aggregation and Visualization:
The DataFrame is grouped by sentiment categories (positive, negative, neutral).
Sentiment distribution is visualized using bar charts with seaborn and matplotlib.
Sentiment Score Distribution:
A function (get_sentiment_score) calculates the sentiment score for each comment (intensity).
The distribution of these scores is visualized to understand the spread and intensity of emotions within the comments.
This sentiment analysis provides insights into audience opinions and emotional responses to the YouTube video.