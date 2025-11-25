# Insightify_Full: Advanced Sentiment \& Keyword Analysis App

Welcome to the **Insightify_Full** project! This application is designed to transform unstructured text data (reviews, comments, social media feedback, etc.) into actionable insights. It provides highly accurate **Sentiment Analysis** and **Keyword Extraction** by leveraging high-performance local **Deep Learning models (BERT)** and features an interactive web interface built with Flask.

***

## Features

* **Data Upload and Preview:** Upload `.xlsx`, `.csv`, or `.json` files to begin the analysis. Displays a preview of the uploaded data.
* **Intelligent Column Detection:** Automatically detects the main text/review column.
* **Advanced Sentiment Analysis (BERT):** Uses a local **BERT** model (via `transformers`) for high-accuracy sentiment classification (**Positive, Negative, Neutral**).
* **Keyword Extraction:** Extracts and ranks the most frequent and relevant keywords and concepts from the dataset.
* **Interactive Visualizations (Plotly):** Displays analysis results (sentiment distribution and keyword frequency) using engaging and rich **Plotly** charts.
* **Data Persistence (PostgreSQL):** Saves all analysis session logs and individual results permanently to a **PostgreSQL** database using Flask-SQLAlchemy.
* **Downloadable Report (PDF,CSV):** (Next planned feature) Generates a compressed ZIP file containing all results and prepared data tables.

***

## How to Run the App

To run the application with full functionality (including the powerful BERT model), you must run two separate servers: the **Flask App** and the **FastAPI BERT API**

### 1. Install Dependencies

Ensure your Python environment is active and install the necessary libraries:

```bash
pip install -r requirements.txt
```


### 2. Configure and Initialize Database

Ensure your PostgreSQL server is running and update the SQLALCHEMY_DATABASE_URI connection string in your app.py. Then, create the necessary tables:

```python
>>> from app import db, app
>>> with app.app_context():
...     db.create_all()
```


### 3. Run the BERT API Server

Open the first Terminal/Command Prompt window and start the sentiment analysis service. Keep this server running:

```bash
uvicorn bert_api:app --reload
```


### 4. Run the Main Flask App

Open a second Terminal/Command Prompt window and start the frontend application:

```bash
python app.py
```

The application will be available at [http://127.0.0.1:5000](http://127.0.0.1:5000).

***

## 📂 Input Data Requirements

Supported File Formats: `.xlsx`, `.csv`, `.json`.
Required Column: Your file must contain at least one text column (e.g., review, comment, text). The app automatically attempts to detect this column.

Supported Language: The current configuration is optimized for English text data to maximize BERT model accuracy.

***

## 📈 Visualizations Available

All visualizations are created using Plotly and offer full interactivity (zooming, hovering, toggling data).

1. Sentiment Distribution
*Type:* Interactive Pie Chart.
Displays the percentage breakdown of sentiment classifications (Positive, Negative, Neutral) determined by the BERT model.
2. Top Keywords Frequency
*Type:* Interactive Horizontal Bar Chart.
Shows the absolute frequencies of the most important keywords extracted from the cleaned text.

***

## ⚙️ Core Files Structure

| File/Folder | Description |
| :-- | :-- |
| `app.py` | Main Flask entry point; handles routing, database configuration, and orchestrates the analysis. |
| `analyzer.py` | The main analysis class: contains the core logic for BERT and VADER analysis, and keyword extraction. |
| `utils.py` | Utility functions for file loading, column auto-detection, and the direct BERT integration. |
| `local_model_api.py` | Separate FastAPI server hosting the BERT model for local inference. |
| `templates/` | Stores HTML templates (e.g., results.html) for the user interface. |
| `static/` | Holds static files (e.g., styles.css) and client-side JavaScript for interactivity. |


***

## 💾 Data Persistence

The application uses PostgreSQL via SQLAlchemy for permanent data storage.

- **AnalysisSession:** Saves upload metadata (filename, timestamp) and summarized results (keywords, sentiment counts,Diverging Sentiment).
- **SentimentResult:** Stores the individual analysis output (Label, Score, Clean Text) for every single text row.

***

## 📧 Contact

For any questions, inquiries, or suggestions, feel free to reach out to the project contributors:

- Name: Ghinwa Allaoui
- Email: allaouighinwa@gmail.com
- GitHub: Ghinwa1981
