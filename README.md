# 16-362 GS Documentation

## Repos to Use (sources & credit)
General Github Repo to refer to: https://github.com/graphdeco-inria/gaussian-splatting?tab=readme-ov-file  
Repo for easy replication in Colab: https://github.com/camenduru/gaussian-splatting-colab?tab=readme-ov-file 

## Initial Steps for Data Preparation & Processing
If processing your own scenes, ensure that there is a directory that the Git COLMAP loader can read. It must follow a specific format if you are not using one of the author's vetted data sources so you can follow instructions to upload your own scenes here:
[Original Repo: Processing your own scenes](https://github.com/graphdeco-inria/gaussian-splatting?tab=readme-ov-file#processing-your-own-scenes) 

After uploading the dataset in this way, you can run the following command to convert the directory into a readable format by the train.py file

    python convert.py -s <location> [--resize] #If not resizing, ImageMagick is not needed

## Dependencies
We worked out of Colab primarily for the high speed and easily accessible resources published online to run GS
Open a Colab notebook and install the following dependencies in this way:

    %cd /content
    !git clone --recursive https://github.com/camenduru/gaussian-splatting
    !pip install -q plyfile
    
    
    %cd /content/gaussian-splatting
    !pip install -q /content/gaussian-splatting/submodules/diff-gaussian-rasterization
    !pip install -q /content/gaussian-splatting/submodules/simple-knn
    
    
    !wget https://huggingface.co/camenduru/gaussian-splatting/resolve/main/tandt_db.zip
    !unzip tandt_db.zip
    
    
    !python train.py -s /content/gaussian-splatting/tandt/train

Instead of the huggingface directory installed here, feel free to change this to the right dataset that you then unzip and pass to the train.py function

## Running the Model
- Refer to the modified train.py and metric.py file that has been uploaded to this repo so that you can plot graphs of L1 loss, EMA Loss for Log, PSNR, SSIM, and LPIPS over the 30,000 iterations that this model runs for
- You will need to replace the existing train.py and metric.py files in the Colab directory generated from the above code in the correct folders with the modified files in this repo so that the right plots can be produced
- You can then use the following commands to train, render, and get metrics for the model on your COLMAP or synthetic dataset. These instructions are all included in the original repo.

      python train.py -s <path to COLMAP or NeRF Synthetic dataset> --eval # Train with train/test split
      python render.py -m <path to trained model> # Generate renderings
      python metrics.py -m <path to trained model> # Compute error metrics on renderings

These help evaluate the train/test split model, show differences between ground truth and rendered images, and produce metrics for PSNR, SSIM, and LPIPS on the model

## Running with DarkGS
Colab file: [Dark GS Colab](https://colab.research.google.com/drive/1Oxr7XY9qAgyjYd5OVZd6ZrvTnGKRj8Xf?usp=sharing)

Follow the same steps shown in the Colab file to install dependencies, download the data, convert the data, and then use train.py. The data we were working with does not entirely work yet given the very specific nature of uploading a directory and formatting the dataset.

