# Chess Insight Engine

A full-stack chess analysis system that converts PGN files to CSV, stores games in MySQL, analyzes openings, middlegames, and endgames using machine learning, reports win/loss correlations, and predicts outcomes and likely moves from any given board position.

---

## Table of Contents
- [Features](#features)
- [System Overview](#system-overview)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup](#setup)
- [Usage](#usage)
- [Outputs](#outputs)
- [Modules & Scripts](#modules--scripts)
- [Planned Enhancements](#planned-enhancements)

---

## Features

### **1. PGN → CSV Conversion**
- Converts raw PGN files into clean CSV format.
- Extracts moves, results, metadata, ECO codes, and timestamps.
- Prepares data for MySQL ingestion.

### **2. MySQL Game Database**
- Stores all converted game data.
- Relational schema optimized for chess-specific queries.
- Indexed for fast analysis on openings, positions, move patterns, and results.

### **3. Statistical Analysis Engine**
Provides:
- Opening win/loss percentages  
- Middlegame structure and pattern evaluation  
- Endgame outcome analysis  
- Color-specific strategy success  
- Strategy correlation reports  

### **4. Machine Learning Engine**
- Converts positions into ML feature vectors.
- Predicts next likely moves for both players.
- Estimates win/loss/draw probability from any FEN position.
- Generates predicted continuation lines.

### **5. Position Evaluation API**
Given:
- FEN string  
- Whose turn (white/black)

Returns:
- Win/loss/draw probability  
- Best predicted moves  
- Most likely opponent moves  
- Opening/middlegame/endgame classification  
- Count of similar historical games  

---

## System Overview

**Overall workflow:**

1. Input PGN dataset  
2. Convert PGN → CSV  
3. Insert CSV into MySQL  
4. Run feature engineering  
5. Generate statistical reports  
6. Train ML model  
7. Provide prediction engine + API  

This system combines:
- A chess database  
- Statistical analysis  
- Machine learning outcome prediction  
- A queryable engine  

---

## Tech Stack

### **Backend**
- Python 3.10+
- MySQL 8.x

### **Data Processing**
- python-chess  
- Pandas  
- Custom PGN parser  

### **Machine Learning**
- TensorFlow or PyTorch  
- Scikit-learn  
- NumPy  

### **API**
- FastAPI  
- JSON responses  

---

## Project Structure
/chess-insight-engine

│── README.md

│── requirements.txt

│

├── pgn_to_csv/

│ └── convert_pgn.py

│

├── database/

│ ├── schema.sql

│ ├── insert_games.py

│ └── queries_example.sql

│

├── analysis/

│ ├── opening_analysis.py

│ ├── middlegame_analysis.py

│ ├── endgame_analysis.py

│ ├── correlation_report.py

│ └── generate_summary.py

│

├── ml/

│ ├── feature_engineering.py

│ ├── train_model.py

│ ├── evaluate_model.py

│ └── predict_position.py

│

└── api/

└── engine_api.py


---

## Setup

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Set Up MySQL Database
```bash
mysql -u root -p < database/schema.sql
```

### 3. Configure Credentials

Edit DB credentials inside:
- insert_games.py
- feature_engineering.py
- engine_api.py

## Usage
### 1. Convert PGN → CSV
```
python pgn_to_csv/convert_pgn.py input.pgn output.csv
```

### 2. Import CSV Into MySQL
```
python database/insert_games.py output.csv
```

### 3. Run Statistical Reports
```
python analysis/opening_analysis.py
python analysis/middlegame_analysis.py
python analysis/endgame_analysis.py
python analysis/correlation_report.py
```
### 4. Train ML Model
```
python ml/train_model.py
```

### 5. Predict From a Chess Position
```
python ml/predict_position.py --fen "<FEN_STRING>" --turn white
```

### 6. Launch API
```
uvicorn api.engine_api:app --reload
```
## Outputs
### Statistical Outputs
- Opening win/loss percentages
- Middlegame positional effectiveness
- Endgame pattern success rates
- Color-based advantages
- Strategy and pattern correlation summaries
- ML Engine Outputs
- Predicted best move for the player
- Predicted likely response from opponent
- Win/loss/draw probability
- Predicted continuation line
- Stage classification: opening / middlegame / endgame

### Example JSON Output

  ```json
  {
  "best_move": "Nf3",
  "likely_opponent_move": "Nc6",
  "win_probability_white": 0.57,
  "win_probability_black": 0.29,
  "draw_probability": 0.14,
  "stage": "opening",
  "similar_games": 8421
}
```

## Modules & Scripts

### pgn_to_csv/
- convert_pgn.py
Converts PGN → CSV with moves, ECO, results, tags.

### database/

- schema.sql — MySQL database structure
- insert_games.py — Loads CSV into MySQL
- queries_example.sql — Example analytics queries

### analysis/

- opening_analysis.py — Opening win/loss percentages
- middlegame_analysis.py — Middlegame strategy evaluation
- endgame_analysis.py — Endgame pattern success rates
- correlation_report.py — Strategy correlation matrix
- generate_summary.py — Human-readable summary reports

### ml/

- feature_engineering.py — Converts positions to ML features
- train_model.py — ML training pipeline
- evaluate_model.py — Tests accuracy of the model
- predict_position.py — Predicts moves & win chance from FEN

### api/

- engine_api.py — FastAPI interface for the prediction engine

## Planned Enhancements

- Interactive web dashboard
- Real-time game advisor
- Chess GUI integration
- Hybrid Stockfish + ML evaluation
- Support for Lichess / Chess.com importing
- Opening repertoire suggestions
- User-based personalized models

## License
