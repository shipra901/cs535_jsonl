# CS535 Project 2 - Dylan Murphey
This project satisfies all requirements in the assignment spec document. The
connected components algorithm is fairly simple, effectively performing a DFS by
comparing the mutual_links dataframe to the vertices dataframe until no new
connections are discovered. Additionally, the program checkpoints every 3
iterations by writing to `{CS535_S3_WORKSPACE}/iter_#`. I'm sure the number
could probably be increased to boost performance a tinge, but it completed in 46
minutes which is well below the maximum and errs on the side of caution.

## Usage - EMR Step
(Assuming mutual_links has already been run using the `CS535_S3_WORKSPACE`
environment variable, which will output in `{CS535_S3_WORKSPACE}/mutual_links`)
- First, create a zip file containing the `project2.py` file
  - `zip.sh`
- Upload `entrypoint.py` and `project2.zip` to S3
  - similar to `upload.sh`
- Run `python3 start_emr.py` after making necessary adjustments

## Test Suite
With `pytest` and `PySpark` as dependencies, simply run `python3 test_suite.py`
to execute the tests. It does a simple pair of asserts on both `mutual_links.py`
and then `connected_components.py` using the synthetic data provided and will
write the resulting parquet files within the `synthetic_data` folder as well.

Simply put, the synthetic data resembles the necessary columns from the
Wikipedia dataset and will result in a table with 3 mutual links, which form 2
connected components (size 2 and 3 vertices).

## Reflection
Probably the most surprising thing I have learned from these projects about the
Wikipedia dataset was just how small the connected components ended up being
outside of the one which included "Anarchism". I thought for sure that there
would be more clusters measured in the thousands for like categories: sports
teams, politicians, et cetera. I suppose many of them are in the mega-component!

As far as what I learned from the assignment, it's primarily that Spark sucks.
I felt like a pediatrician, trying to diagnose what's wrong with a kid that
keeps fussing but can't describe their symptoms. That said, I am very glad that
I gained exposure to Spark and expanded my exposure to AWS because I am sure I
won't be able to avoid at least AWS in my career.
