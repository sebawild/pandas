# Instrumenting pandas

## Building pandas from source

    source ./venv/bin/activate

Checkout https://github.com/sebawild/pandas/tree/1.5.x

Then followed instructions here:
https://pandas.pydata.org/pandas-docs/stable/development/contributing_environment.html#contributing-environment
for pip based environment.

But `pip install -r requirements-dev.txt` fails for a few packages:
 * `numba`: I removed nubma from `requirements-dev.txt` for now (hopefully not necessary, 
   since only a performance improvement)
 * `psycopg2`: I followed the instructions in the error message and list `psycopg2-binary`
   instead of compiling from source.
 * `tables`: seems to have fixed itself!?
 * `pyarrow`: Was `<10`; I used 11 instead ... probably trouble
 * `python-snappy`: Seems to need library  (`sudo apt-get install libsnappy-dev`)
   again, this error just disappeared on second run ... concurrency issues?



Now to build (https://pandas.pydata.org/pandas-docs/stable/development/contributing_environment.html#step-3-build-and-install-pandas)

    python setup.py build_ext -j 4
    python -m pip install -e . --no-build-isolation --no-use-pep517
￼
