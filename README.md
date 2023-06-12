# reddit_praw
**Reddit PRAW**

This repository contains code for scraping headlines from the subreddit 'Tesla' and performing sentiment analysis on the scraped data using the VADER (Valence Aware Dictionary and Sentiment Reasoner) sentiment analysis tool.

**Prerequisites**

To run this code, you need to have the following dependencies installed:

- Python 3.x
- **praw** library
- **pandas** library
- **numpy** library
- **matplotlib** library
- **seaborn** library
- **nltk** library with the **vader\_lexicon** package

You can install the required packages using pip:

pip install praw pandas numpy matplotlib seaborn nltk 

**Setup**

1. Sign up for a Reddit developer account and create an application to obtain the client ID and client secret necessary for using the Reddit API. Replace **"your client id"** and **"your client secret"** in the code with your actual values.

client\_id = "your client id" client\_secret = "your client secret" 

2. Update the **user\_agent** variable with an appropriate user agent string.

user\_agent = "Scrapper 1.0 by demo" 

3. Download the VADER lexicon for sentiment analysis using the NLTK library. Uncomment the following line of code to download the lexicon:

nltk.download('vader\_lexicon') 

**Usage**

The code retrieves the headlines from the 'Tesla' subreddit and performs sentiment analysis on them. It classifies the sentiment of each headline as positive, negative, or neutral based on the compound score obtained from the VADER analysis.

1. Initialize a Reddit instance using the credentials and user agent:

reddit = praw.Reddit( client\_id=client\_id, client\_secret=client\_secret, user\_agent=user\_agent ) 

2. Scrape the headlines from the subreddit:

headlines = set() for submission in reddit.subreddit('Tesla').hot(limit=None):     

headlines.add(submission.title) 

3. Perform sentiment analysis on the headlines using VADER:

sia = SIA() results = [] for line in headlines: pol\_score = sia.polarity\_scores(line)       

pol\_score['headlines'] = line results.append(pol\_score) 

4. Create a Pandas DataFrame to store the sentiment analysis results:

df = pd.DataFrame.from\_records(results) 

5. Classify the sentiment of each headline based on the compound score and assign a label:

df['label'] = 0 
df.loc[df['compound'] > 0.2, 'label'] = 1 # positive comment 
df.loc[df['compound']< 0.2, 'label'] = -1 # negative comment 

6. View the DataFrame with the sentiment analysis results:

df.head() 

**Results**

The DataFrame **df** contains the sentiment analysis results for the scraped headlines. It includes the original headline, along with the compound score and label assigned to each headline.

**Acknowledgments**

- The **praw** library for providing an easy-to-use interface to the Reddit API.
- The **nltk** library for the VADER sentiment analysis tool.
- The Python data science libraries (**pandas**, **numpy**, **matplotlib**, **seaborn**) for data manipulation and visualization.



