# MachineLearningInAstronomy
github repository for `Machine Learning in Astronomy` course in Astronomy, Stockholm University, 2018

## Getting started with astroML hands on sessions
In order for everyone to work together on the hands on sessions, it would be useful to use the same version of software. If you are using anaconda python3, the easiest way to do this is using an environment. If you don't have anaconda, are using python2 or would prefer to use a separate distribution for this class, you can install a new miniconda distribution to `location`:
```
bash ./install/install_python.sh location 
```
The defualt location is `${HOME}/astroml_miniconda3`, which is where it will be installed if you simply type
```
bash ./install/install_python.sh
```
Follow the instructions to remove the miniconda install script and then to use the path (you must do this everytime you want to start in a new shell to use this python (or use the setup script) or add it to your bash profile if you want to use this as a default).

If you used this to install python, it will create `./install/setup.sh`, and every other time you want to use astroml, use
```
source ./install/setup.sh 
```
to use this python and use the astroml environment.

### Using the environment
If you have not installed python as above and prefer to use your own python,  but would like to install the astroml environment:
```
conda env create -n astroml --file environment.yml
``` 
This should show the `solving environment` and then start installing the libraries.

In order to use the `astroml` software, you will have to run 
```
source activate astroml
```
everytime to setup the environment.
