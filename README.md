  <h1>COVID-19 Data Cleaning & Exploratory Analysis</h1>
  <p>This project focuses on cleaning, processing, and analyzing COVID-19 data obtained from WHO.</p>

  <h2>Overview</h2>
  <ul>
    <li>Handle missing values in the dataset</li>
    <li>Reconstruct daily cases and deaths using cumulative counts</li>
    <li>Perform exploratory data analysis (EDA)</li>
    <li>Generate visualizations to extract insights</li>
  </ul>

  <h2>Tools & Libraries</h2>
  <ul>
    <li>Python</li>
    <li>Pandas</li>
    <li>NumPy</li>
    <li>Matplotlib</li>
    <li>Seaborn</li>
  </ul>

  <h2>Data Cleaning Steps</h2>
  <ol>
    <li>Load dataset and inspect missing values</li>
    <li>Sort by Country, WHO_region, Date_reported</li>
    <li>Create lagged columns using shift()</li>
    <li>Fill missing daily cases/deaths using cumulative differences</li>
    <li>Drop minor irrelevant missing values</li>
    <li>Ensure no NaN values remain</li>
  </ol>

  <h2>EDA</h2>
  <ul>
    <li>Line plots: yearly trends of cases and deaths</li>
    <li>Count plot: distribution of cases across WHO regions</li>
  </ul>

  <h2>Insights</h2>
  <ul>
    <li>Strong growth in 2020–2021</li>
    <li>Europe and the Americas show highest cases</li>
    <li>Deaths follow similar pattern but lag behind</li>
  </ul>

  <h2>Future Work</h2>
  <ul>
    <li>Add rolling averages (7-day)</li>
    <li>Correlation analysis between cases and deaths</li>
    <li>Predictive modeling (ARIMA/Prophet)</li>
    <li>Interactive dashboard with Streamlit/Plotly</li>
  </ul>

  <h2>Project Structure</h2>
  <pre>
📦 covid19-analysis
 ┣ analysis.ipynb
 ┣ Covid19.csv
 ┗ README.html
  </pre>

  <h2>Author</h2>
  <p><b>Ahmed Hambuta</b> – Data Enthusiast & Analyst</p>
