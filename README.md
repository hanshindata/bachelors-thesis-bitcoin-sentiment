# Bitcoin Market Sentiment Analysis using KoBERT and Granger Causality

## 📌 Introduction
This project is a bachelor's thesis analyzing the relationship between social media sentiment (from dcinside Bitcoin Gallery) and Bitcoin price dynamics. It utilizes KoBERT for Korean sentiment analysis and Granger Causality for statistical investigation. This repository contains all the code, references to data, and documentation related to this research.

## 📝 Abstract
This study aims to analyze the relationship between sentiment data from social media and Bitcoin price dynamics (including both directional changes and volatility). While previous research has primarily focused on whether sentiment data can predict price fluctuations, this study also considers the impact of price fluctuations on sentiment data. For this purpose, posts from the "dcinside Bitcoin Gallery" were subjected to sentiment analysis, and their relationship with Bitcoin's price dynamics was quantitatively analyzed.

KoBERT, a BERT model specialized for the Korean language, was used for sentiment analysis. After analyzing the sentiment of each post, daily aggregates were computed to derive the proportion of positive sentiment (pos_ratio), negative sentiment (neg_ratio), and neutral sentiment (neu_ratio). As statistical analysis methods, the Granger Causality Test and Correlation Analysis were applied to examine the relationships between sentiment data and key Bitcoin price metrics, specifically price returns (directional changes) and price volatility (defined here as the absolute value of its rate of change).

The results of the experiment did not confirm a significant relationship where sentiment data causes Bitcoin price fluctuations. The Granger Causality Test results showed p-values greater than 0.05 for all sentiment indicators, suggesting that sentiment cannot predict price fluctuations. On the other hand, a strong impact of price fluctuations on sentiment data, particularly negative sentiment (neg_ratio), was observed. Furthermore, a tendency for neutral sentiment (neu_ratio) to decrease as the absolute value of price volatility increases was observed, suggesting that market instability can be a factor in causing extreme shifts in investor sentiment.

This study suggests that sentiment data does not influence price fluctuations, which contrasts with previous research, particularly AI-based sentiment prediction models. Therefore, future research needs to conduct a comparative analysis of this aspect. Additionally, future tasks include collecting data over a longer period, incorporating diverse social media platforms, and considering market event factors in the analysis.

## 🔑 Key Features
- Data Collection: Crawled approximately 1.6 million posts from the dcinside Bitcoin Gallery for the period March 2024 - January 2025.
- Preprocessing Pipeline: Includes steps for deduplication, date format validation, and specific period extraction (April-September 2024 for main analysis).
- Sentiment Analysis: Fine-tuned KoBERT model for Korean sentiment classification (Positive, Negative, Neutral) on post titles. Achieved 70.4% validation accuracy.
- Statistical Analysis: Applied Granger Causality tests and Pearson correlation to investigate the lead-lag relationship between aggregated sentiment scores and Bitcoin price dynamics.

## 🛠️ Technology Stack
- **Programming Language:** Python 3.x
- **Data Collection:** Selenium, BeautifulSoup4
- **Data Manipulation & Analysis:** Pandas, NumPy
- **Natural Language Processing (NLP) / Sentiment Analysis:**
    - Korean Sentiment Analysis using [KoBERT](https://github.com/SKTBrain/KoBERT) (SKTBrain)
    - Hugging Face Transformers library
    - PyTorch (as backend for Transformers)
- **Statistical Tests:** Statsmodels (for Granger Causality, Pearson Correlation)
- **Environment:** Jupyter Notebooks

## 📂 Project Structure
```
bachelors-thesis-bitcoin-sentiment/
├── .gitignore
├── LICENSE
├── README.md                       # Main project README (You are here!)
├── notebooks/                      # Jupyter notebooks for each processing step
│   ├── 01_dcinside_crawler.ipynb
│   ├── 02_deduplicate_data.ipynb
│   ├── 03_filter_invalid_dates.ipynb
│   ├── 04_extract_6month_period.ipynb
│   ├── 05_kobert_baseline_performance_test.ipynb
│   ├── 06_random_sample_for_labeling.ipynb
│   ├── 07_kobert_sentiment_finetuner.ipynb
│   └── (Additional analysis notebooks - Work in Progress)
├── data/
│   └── README_data.md              # Detailed explanation of the original dataset and why it's not included
├── models/
│   └── README.md                   # Information regarding trained models (not included due to size)
└── requirements.txt                # Python dependencies
```

## ⚙️ Setup and How to Run
This project uses Python and Jupyter Notebooks. The primary goal of providing this code is to showcase the methodology and analytical process used in the bachelor's thesis.

### Prerequisites
* Python 3.x (Developed with Python 3.9)
* pip (Python package installer)

### Environment Setup
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/hanshindata/bachelors-thesis-bitcoin-sentiment.git
    cd bachelors-thesis-bitcoin-sentiment
    ```
2.  **Create and activate a virtual environment (recommended):**
    ```bash
    python -m venv venv
    # On macOS/Linux:
    source venv/bin/activate
    # On Windows:
    # venv\Scripts\activate
    ```
3.  **Install dependencies:**
    All required Python packages are listed in `requirements.txt`.
    ```bash
    pip install -r requirements.txt
    ```

### Running the Notebooks
The Jupyter Notebooks located in the `notebooks/` directory are numbered sequentially (e.g., `01_...ipynb`, `02_...ipynb`) to represent the data processing and analysis pipeline.

**Important Note on Data and Executability:**
* The notebooks were originally run on a large, private dataset collected from dcinside Bitcoin Gallery.
* **This repository does not contain the full raw or processed datasets due to their size, copyright considerations, and the potentially sensitive nature of the original user-generated content.** Please refer to `data/README_data.md` for a detailed description of the data used in the original research.
* As such, while the code for each step is provided for methodological transparency, executing the notebooks (especially those involving NLP tasks like KoBERT fine-tuning or sentiment prediction) **will not reproduce the results presented in the thesis without access to the original dataset or a similarly structured dataset with actual text content.**
* The notebooks are primarily intended to demonstrate the code logic, data transformations, and analytical steps performed. Key findings and results from the analysis on the full dataset are presented in the "📊 Key Results & Visualizations" section of this README.

## 📊 Key Results & Visualizations

### Sentiment Analysis Performance
- The fine-tuned KoBERT model achieved a validation accuracy of **70.4%** for 3-class sentiment classification (Positive, Negative, Neutral) on Korean Bitcoin-related online community posts.
- *(Detailed classification report including Precision, Recall, and F1-scores for each class will be added soon.)*

### Relationship between Sentiment and Price
1.  **Impact of Price Dynamics on Sentiment:**
    * Granger Causality tests indicated that Bitcoin price drops are followed by a statistically significant increase in subsequent negative online sentiment (neg_ratio) (p-value < 0.05).
    * Increased absolute Bitcoin price volatility (absolute rate of change) was observed to correlate with a decrease in neutral sentiment (neu_ratio), suggesting market instability may polarize investor reactions.

2.  **Impact of Sentiment on Price Changes:**
    * No statistically significant evidence was found to suggest that the analyzed sentiment metrics (pos_ratio, neg_ratio, neu_ratio) can predict subsequent Bitcoin price changes (all p-values > 0.05 in Granger Causality tests).
    * This finding contrasts with some previous studies that utilized AI models for sentiment-based price prediction, indicating a need for further comparative research.

⏳ **Work in Progress:** *Key visualizations and detailed summaries of results will be populated here as they are finalized.* ⏳

## 🚧 Limitations
* The sentiment analysis was primarily based on post titles from a single online community (dcinside Bitcoin Gallery), which may not capture the full nuance of discussions or represent broader market sentiment.
* External market events, regulatory news, or macroeconomic factors that could influence both sentiment and price were not explicitly controlled for in this analysis.
* The dataset covers a specific period (March 2024 - January 2025 for collection, April - September 2024 for main analysis), and findings may not generalize to other timeframes or market conditions.

## 💡 Future Work
* Extend data collection to a longer period and include diverse social media platforms (e.g., X, Reddit) and news articles.
* Incorporate full post content and comments for a more in-depth sentiment analysis.
* Investigate the impact of specific, categorized market events (e.g., policy changes, major exchange news) on both sentiment and price volatility.
* Conduct a comparative analysis with other studies, especially those finding predictive power from sentiment to price, to understand differing outcomes.

## 👨‍💻 Developer Information
- **Name**: HAN SHIN (韓 信)
- **GitHub**: [hanshindata](https://github.com/hanshindata)
- **Email**: han.shin.data@gmail.com
