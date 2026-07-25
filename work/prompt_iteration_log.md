# 📋 FL-01 Task Optimization: Prompt Iteration Log & Cross-Model Audit

**Track:** General AI Fluency / Machine Learning Foundations  
**FL-01 Audit Target Task:** Task 1 — Refactoring & Optimizing Recommendation Algorithms (CollabIn Internship)  
**File Path:** `work/prompt_iteration_log.md`  

---

## 🎯 Target Task Overview
* **Original Task:** Refactor an in-memory Pandas user-interaction scoring loop (1.8 GB CSV / 4.2M rows) taking 84.3 seconds into an optimized DuckDB SQL execution pipeline to achieve sub-2-second local iteration speed without exceeding RAM constraints.

---

## 🛠️ Prompt Iteration Trail (Versions 0 – 5)

### 🛑 Version 0: Naive Baseline
* **Technique Applied:** None (Naive Baseline)
* **Prompt:**
  > `"Write python code to optimize recommendation scoring."`

#### Output Excerpt
```python
import pandas as pd

def score_recommendations(df):
    df['score'] = df['views'] * 0.3 + df['clicks'] * 0.7
    return df.sort_values(by='score', ascending=False)

# Load data and score
df = pd.read_csv('user_interactions.csv')
ranked_df = score_recommendations(df)
print(ranked_df.head())

"Act as a Senior Data Engineer specializing in high-throughput query optimization, vectorized execution, and DuckDB backend architecture. Write python code to optimize recommendation scoring."

import duckdb
import pandas as pd

class RecommendationEngine:
    """High-throughput recommendation scoring engine using DuckDB."""
    def __init__(self, db_path: str = ":memory:"):
        self.con = duckdb.connect(db_path)

    def calculate_scores(self, interaction_table: str):
        query = f"""
            SELECT user_id, item_id,
                   (views_count * 0.3 + clicks_count * 0.7) AS weighted_score
            FROM {interaction_table}
            ORDER BY weighted_score DESC
        """
        return self.con.execute(query).df()

    "Act as a Senior Data Engineer specializing in high-throughput query optimization, vectorized execution, and DuckDB backend architecture. \n\nContext & Motivation: Our backend squad at CollabIn iterates on multi-factor recommendation weights across a 1.8 GB user-interaction dataset (4.2 million rows). Processing this matrix using legacy Pandas .apply() lambdas takes 84.3 seconds per run and pushes local RAM to the brink of crashing. We need a lightweight, in-process DuckDB pipeline that executes directly over raw CSV files and returns top-k recommendations in under 2 seconds to establish a real-time local testing loop.\n\nWrite python code to optimize recommendation scoring."

    import duckdb
import time

def run_optimized_recommendation_scoring(csv_path: str, top_k: int = 100):
    start_time = time.time()
    con = duckdb.connect()
    
    # Direct zero-copy query over 1.8GB raw CSV using DuckDB virtual view
    query = f"""
        SELECT 
            user_id, 
            item_id,
            (interaction_count * 0.4 + implicit_rating * 0.6) AS final_score
        FROM read_csv_auto('{csv_path}')
        WHERE interaction_count > 0
        ORDER BY final_score DESC
        LIMIT {top_k}
    """
    
    result_df = con.execute(query).df()
    print(f"Execution Completed in {time.time() - start_time:.2f} seconds.")
    return result_df

"Act as a Senior Data Engineer specializing in high-throughput query optimization, vectorized execution, and DuckDB backend architecture. Context & Motivation: Our backend squad at CollabIn iterates on multi-factor recommendation weights across a 1.8 GB user-interaction dataset (4.2 million rows)... \n\nFollow this exact optimization transformation pattern:\n\n[BAD PATTERN - In-Memory Pandas]:\n# df['score'] = df.apply(lambda row: row['a']*0.2 + row['b']*0.8, axis=1)\n\n[GOOD PATTERN - Vectorized DuckDB SQL]:\n# duckdb.query('SELECT user_id, item_id, (a * 0.2 + b * 0.8) AS score FROM read_csv_auto(\"data.csv\") ORDER BY score DESC LIMIT 50').df()"

import duckdb

def calculate_weighted_recommendations(file_path: str, weight_views: float = 0.3, weight_clicks: float = 0.7, limit: int = 50):
    # Vectorized SQL transformation following memory-mapped streaming pattern
    sql_query = """
        SELECT 
            user_id,
            item_id,
            (view_count * $weight_views + click_count * $weight_clicks) AS dynamic_score
        FROM read_csv_auto($file_path)
        ORDER BY dynamic_score DESC
        LIMIT $limit
    """
    
    return duckdb.query(sql_query, params={
        'weight_views': weight_views,
        'weight_clicks': weight_clicks,
        'file_path': file_path,
        'limit': limit
    }).df()

"Act as a Senior Data Engineer... Output Constraints:\nReturn a single production-ready Python module structured strictly as follows:\n1. Docstring detailing latency targets and memory boundaries.\n2. Main execution function with strict type hinting.\n3. Benchmark block under if __name__ == '__main__': that constructs mock data, runs the query, and prints RAM usage & execution time."

"""
Module: recommendation_scoring_engine.py
Target Latency: < 2.0 seconds over 4.2M rows (1.8 GB CSV)
Memory Strategy: Zero-copy disk streaming via DuckDB engine
"""

import time
import psutil
import duckdb
import pandas as pd

def compute_recommendations(csv_path: str, w_views: float = 0.3, w_clicks: float = 0.7, limit: int = 100) -> pd.DataFrame:
    query = """
        SELECT user_id, item_id, (views * $1 + clicks * $2) as score
        FROM read_csv_auto($3)
        ORDER BY score DESC LIMIT $4
    """
    return duckdb.execute(query, [w_views, w_clicks, csv_path, limit]).df()

if __name__ == "__main__":
    process = psutil.Process()
    mem_before = process.memory_info().rss / (1024 * 1024)
    start = time.perf_counter()
    
    # Run test
    print(f"Initial Memory: {mem_before:.2f} MB")
    print(f"Benchmark completed in {time.perf_counter() - start:.4f}s")

    "Act as a Senior Data Engineer... Before outputting the final Python code, break down your technical reasoning step-by-step:\nStep 1: Explain the physical I/O bottleneck of Pandas read_csv vs DuckDB read_csv_auto.\nStep 2: Detail how column-oriented scanning avoids loading unneeded interaction columns.\nStep 3: Show the exact vectorized SQL scoring formula.\nStep 4: Output the complete, production-ready Python script."

    ### STEP DECOMPOSITION & TECHNICAL REASONING

Step 1: Physical I/O Bottleneck Analysis
Pandas `.read_csv()` allocates memory for every row and column upfront, creating an in-memory footprint up to 3x the raw CSV size (1.8 GB -> ~5.4 GB RAM), triggering OS page swapping and 80s+ latencies. DuckDB uses memory-mapped file handles to stream chunks directly.

Step 2: Column-Oriented Filtering
The query selects only `user_id`, `item_id`, `views`, and `clicks`. DuckDB's columnar scanner skips all other metadata columns in the 1.8 GB CSV, cutting scanned disk bytes by over 60%.

Step 3: Vectorized Scoring Execution
Scoring is executed natively in C++ SIMD vector batches using `(views * w1 + clicks * w2)`. Sorting is performed in DuckDB's streaming top-k heap without materializing the full result array.

Step 4: Production Python Module
[Complete Python Script Executed Cleanly]

Role & Persona:
Act as a Senior Data & Backend Engineer specializing in high-throughput query optimization, vectorized execution engines, and column-oriented databases ([ENGINE_NAME, e.g., DuckDB / Polars / ClickHouse]).

Context & Motivation:
We are optimizing an execution loop over a [DATASET_SIZE, e.g., 1.8 GB / 4.2M rows] dataset. The current legacy pipeline using [SLOW_METHOD, e.g., Pandas .apply()] takes [CURRENT_LATENCY, e.g., 84.3s] and pushes memory limits. We need an optimized, in-process streaming pipeline that executes directly over raw files and returns top-k results in under [TARGET_LATENCY, e.g., 2.0s].

Optimization Pattern (Few-Shot Reference):
- Avoid: [BAD_PATTERN, e.g., df['score'] = df.apply(lambda row: row['a']*0.3 + row['b']*0.7, axis=1)]
- Prefer: [GOOD_PATTERN, e.g., duckdb.execute("SELECT id, (a*0.3 + b*0.7) AS score FROM read_csv_auto('data.csv') ORDER BY score DESC LIMIT 100")]

Step Decomposition Instructions:
Before generating code, break down your technical analysis:
1. Identify the primary memory and I/O bottlenecks in the current approach.
2. Explain the vectorization or column-pruning strategy used to hit performance targets.
3. Provide the full, runnable Python script with type hints, docstrings, and a performance benchmark block (`psutil` memory + latency timer).

Output Requirements:
Return a single, well-documented Python file following PEP 8 standards with zero conversational fluff.
