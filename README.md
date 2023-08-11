# BoXHED2.0

**B**oosted e**X**act **H**azard **E**stimator with **D**ynamic covariates v2.0 (BoXHED2.0, pronounced 'box-head') is a software package for nonparametrically estimating hazard functions via gradient boosted trees. BoXHED2.0 accommodates both time-static and time-dependent covariates.

Please refer to the [BoXHED2.0 paper](https://arxiv.org/abs/2103.12591) for details, which builds on the [BoXHED1.0 paper](http://proceedings.mlr.press/v119/wang20o/wang20o.pdf) (ICML 2020). The theoretical underpinnings for BoXHED is provided [here](https://projecteuclid.org/journals/annals-of-statistics/volume-49/issue-4/Boosted-nonparametric-hazards-with-time-dependent-covariates/10.1214/20-AOS2028.full) (Annals of Statistics 2021).

What’s new (over BoXHED1.0):
 - Allows for survival data beyond right censoring, including recurrent events
 - Significant speed improvement
 - Multicore CPU and GPU support

## Prerequisites
The software was developed and tested in Linux, Mac OS, and Windows10 environments. The requirements are the following:
- Python (=3.8)
- conda  (we recommend using the free [Anaconda distribution](https://docs.anaconda.com/anaconda/install/))


## Setting up BoXHED2.0
1. Windows users need to have the Visual Studio 17 2022 toolset installed.
   During installation, under the "Workloads" tab select "Desktop Development with C++" in the "Desktop and Mobile" section. Make the following selections in the menu that shows up on the right:
![sc__](https://user-images.githubusercontent.com/34462617/201495851-c7d02796-31e0-4181-9eba-78065d2a5f59.png)

2. Download the prebuilt BoXHED2.0 packages, based on your operating system and architecture from the following list:
* [BoXHED Linux CPU](https://www.dropbox.com/scl/fi/bi5bkae5ahzedej5gskdl/boxhed_linux_cpu.zip?rlkey=il9zv150xncw5awk9i7hhvzu4&dl=0)
* [BoXHED Linux GPU](https://www.dropbox.com/scl/fi/f5b51d3njlr61fjpk98w0/boxhed_linux_gpu.zip?rlkey=l41bb5egv9ies5v48mvcs20f2&dl=0)
* [BoXHED Win10 CPU](https://www.dropbox.com/scl/fi/kpz0y8ko7s4aqwdpx5gwu/boxhed_win10_cpu.zip?rlkey=qgy4mkbl78b4vk73tg1m8t32q&dl=0)
* [BoXHED Win10 GPU](https://www.dropbox.com/scl/fi/wxqfsztoogdsawcev0b6o/boxhed_win10_gpu.zip?rlkey=vc22sgypo9c2oqf2kvkgdhvip&dl=0)
* [BoXHED OSX CPU M1](https://www.dropbox.com/scl/fi/2rztizbhhm7h8rigl2gmb/boxhed_osx_cpu_M1.zip?rlkey=q9232o0pphhd0eoq5ggbiyzhk&dl=0)
  
  This step will download a .zip file in your Downloads folder, if you haven't selected any other directory for the downloaded file.

3. Set up a dedicated virtual environment for BoXHED2.0. This ensures that BoXHED2.0 will not interfere with any existing XGBoost packages. This implementation uses python 3.8. In this example we use [Anaconda Prompt](https://docs.anaconda.com/anaconda/install/) to open a terminal. First, create a virtual environment called boxhed2:
```
conda create -n boxhed2 python=3.8
```

then activate it
```
conda activate boxhed2
```

4. Install the dependencies by pasting the following lines in your terminal:
```
pip install matplotlib==3.7.1
pip install pillow==9.4.0
pip install numpy==1.24.3
pip install scikit-learn==1.2.2
pip install pytz==2023.3
pip install pandas==1.5.3
pip install cmake==3.26.3
pip install py3nvml==0.2.7
pip install tqdm==4.65.0
pip install threadpoolctl==3.1.0
pip install scipy==1.10.1
pip install joblib==1.2.0
pip install --force-reinstall --upgrade python-dateutil
pip install jupyter
```

Mac users need to additionally install OpenMP to use multithreaded CPU operation. Without OpenMP BoXHED2.0 uses a single CPU core, leading to suboptimal runtime:
```
brew install libomp
```

5. To find where the downloaded BoXHED2.0 files need to be put, run the following line:
```
python -c "import sys; site_packages = next(p for p in sys.path if all([k in p for k in ['boxhed2', 'site-packages']])); print(site_packages)"
```

Running the line above prints a directory in the terminal. For example, the following directory gets printed:
```
/home/grads/d/j.doe/anaconda3/envs/boxhed2/lib/python3.8/site-packages/
```

6. In step 2 you downloaded a .zip file. In step 5 we identified a directory. Now copy the folders inside the .zip file into the directory identified in step 5.
After copying the files over, the following folders need to exist:
```
/home/grads/d/j.doe/anaconda3/envs/boxhed2/lib/python3.8/site-packages/boxhed/
/home/grads/d/j.doe/anaconda3/envs/boxhed2/lib/python3.8/site-packages/boxhed_kernel/
/home/grads/d/j.doe/anaconda3/envs/boxhed2/lib/python3.8/site-packages/boxhed_prep/
/home/grads/d/j.doe/anaconda3/envs/boxhed2/lib/python3.8/site-packages/shap/
```

7. Back in the terminal, clone this repository by running:
```
git clone https://github.com/BoXHED/BoXHED2.0_.git
```

8. Go to the directory BoXHED2.0_:
```
cd BoXHED2.0_
```

9. Run *BoXHED2_tutorial.ipynb* for a demonstration of how to fit a BoXHED hazard estimator.
```
jupyter notebook BoXHED2_tutorial.ipynb
```
