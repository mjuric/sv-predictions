# Analysis scripts

The scripts inside this folder are used for analysing and visualizing the simulation data.

REQUIREMENTS
  - numpy
  - pandas
  - matplotlib
  - astropy
  - astroquery.jplhorizons
  - ffmpeg

These scripts require aditional files in order to run, to download them, take a look at the README file in the `../data` folder.

To find the instructions on how to use the scripts in this folder take a look at the information below:

## obs-viz.ipynb

This script is made for visualizing Vera Rubin's science validation survey. To run this script you will need to put the `sv_20250729.db` file in your `../data` directory. To get this file, please cnsult the `README` file in the `../data` directory.
After running, the script should output a movie titled: `sv-viz.mp4` in the `../results` directory. The generated frames of this movie are located in the `../results/sv-viz` directory.

## asteroid-viz.ipynb

This script is made for visualizing positions of simulated asteroids in the night sky as well as creating a sky map of observed known asteroids. It outputs a movie titled `simulated_asteroids.mp4` in the `../results` folder, the files necessary for creating the sky map of known asteroids are located inside `../results/real_data`, and the files of simulated asteroids are inside the `../results/sim-outputs` directory. The generated frames of this movie are located in the `../results/simulated_asteroids`
