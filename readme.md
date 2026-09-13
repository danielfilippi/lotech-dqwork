# Desc

I have done 1 markdown file and 1 notebook per task (except A which has 3 notebooks)

The markdowns contain my raw thinking process/train of thought, and the notebooks follow the same order. 

I had the doc and the notebook side by side as I was working through these tasks, so I would urge you to do the same as you review!

Thank you

## Running the notebooks

Requires Python 3.13. I have not included the parquet files in the repo because this is not my data. Please put them in /parquets

run in powershell at root :

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyterlab
```

Open the notebooks in `notebooks/` and run their cells from top to bottom.

### Exercise A run order

1. `a_topofbook_initial.ipynb`
2. `a_trades_initial.ipynb`
3. `a_joined.ipynb`

The last notebook relies on the output of the first two

### Other exercises

The other notebooks can be run as is

Exercise D includes both an initial approach and `d_secondtry.ipynb`. The report explains why the first approach was rejected

Reports are in `docs/`, labelled by exercise letter.
