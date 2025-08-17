# Simulation files

`MAIN_SIMULATOR`   (formerly known as pas)

REQUIREMENTS
pandas
numpy
tqdm
subprocess
multiprocessing
sorcha
environment - this line updates the system PATH variable to include the custom environment where sorcha is installed
base directory
file prefix
Create a Folder
Inside the folder create folders: colors, orbits and output
In the output folder create folders: e2e and stats
Open `main_simulator.ipynb`
`BASE-DIR` as path to the folder
The expected names of the files are  `{file_prefix}orbits.csv` and `{file_prefix}colors.csv` in the folder
The colors.csv should have the following columns: ObjID, H-r, u-r, g-r, i-r, z-r, y-r, GS
The orbits.csv should have the following columns: ObjID, FORMAT, g, e, inc, node, argPeri, ma, epochMJD_TDB
Function splitfile (splits the file). The arguments are the csv file to be split, the output directory and the number of files it will be split into. The files it returns will be roughly the same size.

to find out more, go to: https://sorcha.readthedocs.io
https://sorcha.readthedocs.io
`i` is the number of the chunk chosen
it will run the sorcha command
file `{BASE-DIR}/colors{file-prefix}colors.csv_split_{i}.csv`
file `{BASE-DIR}/orbits/{file-prefix}orbits.csv_split_{i}.csv`
put it in output in folders `e2e` and `stats`
change the pointing data base
`indices = range(1,150)`
run everything in order
The script runs the `run_sorcha` function on chunks numbered 1 to 150 it shows the progress bar via tqdm

`merge_csv_files(folder_path, output_file)`
We merge the chunks we ran sorcha
The arguments are the path of the folder and the output file they will be merged into
we do it for `e2e` and `stats`

`FILEFIXER`    (formerly known as riba)
The required package is pandas
`df` = data frame, expected format`{BASE_DIR}/large_neo_input.h5`
`df_every_10th`  it makes it smaller 10 times
`df_every_10th.tocsv` converts to csv
`df_orbits`is the header row of the list orbits.csv
`df_colors` is the header row of the list colors.csv
`df_colorfix` replaces the data in the columns with the data that we took from the population analysis

`FORMAT_CONVERTER`    (formerly known as macka)
the required packages are the same as the
`l` is the list of prefixes from the data
The `for loop` goes through the orbits files of the data, converts it to csv and prints the first few rows of the table of the file with the current sufix
`merge_csv_file()` is the same as in the `main_simulator` notebook
