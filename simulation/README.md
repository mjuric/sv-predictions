# Simulation files

`MAIN_SIMULATOR`   (formerly known as "pas" or dog in english)

REQUIREMENTS
- pandas
- numpy
- tqdm
- subprocess
- multiprocessing
- sorcha


You need to have Sorcha installed and it needs to be in the same environment as the notebooks. For installing, you can go to the website: https://sorcha.readthedocs.io (we recommend using mamba instead of conda)
We downloaded the real data from https://epyc.astro.washington.edu/~mjuric/mpsky-data-dev/catalogs/ which are the processed files originally from https://minorplanetcenter.net/ and the simulated data from https://www.canfar.net/storage/vault/list/AstroDataCitationDOI/CISTI.CANFAR/25.0062/data 
 
SETUP
1. Create a `Folder`
2. Put the data inside the `Folder`
3. The pointing database we used can be found here: https://survey-strategy.lsst.io/progress/sv_status/sv_20250729.html , you need to download it to the same `Folder`
4. Inside the `Folder` create folders: colors, orbits and output
5. In the output folder create folders: e2e and stats
6. Open `main_simulator.ipynb`
7. `BASE_DIR`is the  path to the `Folder`
8. The expected names of the files we will use are in the form `{file_prefix}orbits.csv` and `{file_prefix}colors.csv`
9. `os.environ["PATH"]` = you need to add your virtual environment to the path


10. The colors file should have the following columns: `ObjID, H-r, u-r, g-r, i-r, z-r, y-r, GS`
11. The orbits file should have the following columns: `ObjID, FORMAT, g, e, inc, node, argPeri, ma, epochMJD_TDB`
12. Function `splitfile(input_file, output_dir, n)` splits the file. The arguments are: the csv file to be split, the output directory and the number of files it will be split into. The files it returns will be roughly the same size.

SIMULATION
Function `run_sorcha(i)`:
`i` is the number of the chunk chosen to run the sorcha command on
`-o {BASE_DIR}/output/ -t e2e/e2e_{i} --stats stats/stats_{i}` puts the output in folders `e2e` and `stats`
`--pointing-db sv_20250729.db` sets the pointing data base

We use the function as worker to run all the chunks simultaneously with multiprocess.

`indices = range(1,n+1)`, n being the number of the chunks:
The script runs the function on chunks numbered 1 to n+1, and shows the progress bar via tqdm.

OUTPUT
`merge_csv_files(folder_path, output_file)`:
We merge the chunks we recieved from sorcha. The arguments are the path of the folder and the output file they will be merged into.
Here we do it for `./output/e2e/` and `./output/stats/` and save the two files into `./output/`.





`FILEFIXER`    (formerly known as riba or fish in english)

The required package is pandas
`df` = data frame read from a file we wish to process
`df_every_10th` the shrinked version by a factor of 10
`df_every_10th.to_csv` converts processed `df` to a csv file
`df_orbits` selected columns needed for `orbits.csv`
`df_colors` selected columns needed for `colors.csv`
`df_colorfix` replaces the data in the columns with the data that we took from population analysis data





`FORMAT_CONVERTER`    (formerly known as macka or cat in english)
This file is specialised for processing the TNO simulated data which needed some extra work.

The required packages are the same as for the `main_simulator`
`l` is the list of prefixes found in the processed population from the data.
The `for loop` goes through the orbits files of the data, converts it to csv and prints the first few rows of the table of the file with the current sufix
`merge_csv_file()` is the same as in the `main_simulator` notebook
