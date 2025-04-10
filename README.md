# Leaf Detect app

Streamlit app for leaf segmentation.

## Getting Started
+ You can run the app locally on your machine, which requires installing Docker.
+ Alternatively, you can run the app on the CyVerse Discovery Envrionment. Instructions for running on CyVerse can be found on [HackMD](https://hackmd.io/G-wdHhh-Rz6JE4RR7m5JCw).

### To Run locally

I recommend to create a project folder `leaf-segmentation` that will contain 3 directories:

1. this github repository (`leaf-detect`)
2. directory containing ML model files (`models`)
3. directory containing data (`data`)


So first, create the directory for the project, create the `data` and `models` folders, and clone the git repository into the project folder.
```
$ mkdir leaf-segmentation 
$ cd leaf-segmentation
$ mkdir data
$ mkdir models
$ git clone git@github.com:ua-srp-dmac/leaf-detect.git
```

Then, populate your folders with these example data/models stored on [CyVerse here](https://de.cyverse.org/data/ds/iplant/home/shared/srp_dmac/leaf_detect_dataset). You'll need to create a free CyVerse account [here](https://user.cyverse.org/signup).  Please refer to [Transferring Data with Cyberduck](https://learning.cyverse.org/ds/cyberduck/) to download data from CyVerse.

Once you have your folders populated, you can build and run the docker container from the `leaf-detect` directory. You'll need to replace `<your-dockerhub-username>` with your own username and replace the `/path/to/data` and `path/to/models` with the full path to the data/models folders that you just created.

```
$ cd leaf-detect
$ docker build -t <your-dockerhub-username>/leaf-detect:latest .

$ docker run --rm -e PYTHONUNBUFFERED=1 -v /path/to/leaf-segmentation:/data-store -p 8501:8501 <your-dockerhub-username>/leaf-detect:latest -d data -m models/leaf_qr_model.pth -r results
```

We mount to the `/data-store/` directory because thsi app is designed to be deployed as a CyVerse VICE app and this is how VICE apps access files from the Data Store.

The streamlit app can then be accessed at `http://localhost:8501`.