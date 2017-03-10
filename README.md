#Compound Figure Separator

This repository contains an implementation of compound figure separator using a covolutional neral network (CNN). 

##Requirements
tensorflow 1.0  https://www.tensorflow.org
opencv 3 http://opencv.org
and some more packages.  
```
pip install tensorflow
#pip instal tensorflow-gpu #in case you want to use GPU
conda uninstall -c menpo opencv #in case you have opnecv2
conda install -c menpo opencv3
```

##Citation
If you find this tool useful, please consider to cite: 
```
@article {...}
```

##Another requirement: pretrained model
Let's donwload the pretrained model at the `./data` directory. I uploaded onto multiple places. 
Google Drive: [https://drive.google.com/open?id=0B046sNk0DhCDems2am5YV3NLeDQ](https://drive.google.com/open?id=0B046sNk0DhCDems2am5YV3NLeDQ)  
Dropbox: [https://dl.dropboxusercontent.com/content_link/QQFaBjkB4xv5wn5GiRAMAWjWqdZOmTmE5B46sfOskG66gZEl6zcmDaNaE5HM4nDl/file?dl=1](https://dl.dropboxusercontent.com/content_link/QQFaBjkB4xv5wn5GiRAMAWjWqdZOmTmE5B46sfOskG66gZEl6zcmDaNaE5HM4nDl/file?dl=1)


##I just want to separate compound figures. 
Sure, just use this command:
```
python main.py --images ~/imgs --output  annotate 1
```
See the results directory. You have sub-figures at ./results . That's it! 

Here is other options:
```
  --images IMAGES      the directory that has figures
  --model MODEL        model pb file. Default is ./data/figure-sepration-model-submitted-544.pb
  --thresh THRESH      sub-figuere detection threshold. Default is 0.5
  --output OUTPUT      output directory ./results
  --annotate ANNOTATE  save annotation to the image or not. 1 is yes, 0 is no. Default is 0.
  ```

 Output json is somethine like:
```
[
 {
 "x": (x coordinate of left top point of the sub-figure),
 "y": (y coordinate of left top point of the sub-figure),
 "w": (width of the sub-figure),
 "h": (height of the sub-figure),
 "conf": (confidence value of the extaction),
 } ,....
] 
```

##I want to use inside my own code
Sure. You can use `FigureSeparator` class. See `simple_example.py` which is:
```
from code.FigureSeparator import FigureSeparator
fig_separator=FigureSeparator("./data/figure-sepration-model-submitted-544.pb")
sub_figures=fig_separator.extract("./imgs/PMC4076561-Figure5-1.png")
print(sub_figures)
```
Giving you the bounding box of sub-figures with confidence values. 

##Acknowledgements
The training is done by [darknet](https://github.com/pjreddie/darknet) and then ported to tensorflow model using [darkflow](https://github.com/thtrieu/darkflow). Part of the code is re-used from darkflow. Thank you very much for the authors of these two repositories. 