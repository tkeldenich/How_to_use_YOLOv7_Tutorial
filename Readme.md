# **How to use YOLOv7 ? – Best Tutorial Simple**

*   [English Article](https://inside-machinelearning.com/en/use-yolov6/)
*   [French Article](https://inside-machinelearning.com/utiliser-yolov6/)

YOLOv7 is the second version of YOLO to be published this year 2022.

**YOLO stands for You Only Look Once. It is a Deep Learning model used for detection on images and videos.**

The first version of YOLO was released in 2016. Since then, frequent updates are made with the latest improvements: faster computation, better accuracy.

We've already a tutoriel on [how to use YOLOv6](https://inside-machinelearning.com/en/use-yolov6/). This post will be pretty similar as we want to stick to the basics.

We'll use the same image as a test to compare both models performance... but keep in mind, performance on one image isn't performance of the entire model. It's just a nice hint to start understand both models.

Let's get to it !

## **How to use YOLOv7 ?**

*Please during this tutorial you'll see `&> /dev/null` at the end of any command starting by "!". This is use to hide the command output and make the tutorial more legible. Thus it also hide any error. Feel free to remove it!*

To use YOLOv7, we first need to download the Github repository!

In order to do this, we’ll use the `git clone` command to download it to our Notebook:


```python
!git clone https://github.com/WongKinYiu/yolov7.git &> /dev/null
```

Then, we place ourselves in the folder we just downloaded:


```python
%cd yolov7
```

    /content/yolov7


Next, we have to install all the necessary libraries to use YOLOv6.

Main libraries are the following:

*   matplotlib
*   numpy
*   opencv-python
*   Pillow
*   PyYAML
*   requests
*   scipy
*   torch
*   torchvision
*   tqdm
*   protobuf

Fortunately, only one line of code is needed to install all these dependencies:


```python
!pip install -r requirements.txt &> /dev/null
```

We then want to download the weights of the Neural Network.

**With the `git clone` command, we’ve downloaded all the architecture of the Neural Network (layers of the model, functions to train it, use it, evaluate it, …) but to use it, we also need the weights.**

> In a Neural Network, the weights are the information obtained by the model during training.

You can manually download any version of the weights [here](https://github.com/wongkinyiu/yolov7/releases) and then put the file in the yolov7 folder.

Or easily download it with this line of code:


```python
!wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-e6e.pt
```

    --2022-07-14 09:48:50--  https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-e6e.pt
    Resolving github.com (github.com)... 140.82.114.3
    Connecting to github.com (github.com)|140.82.114.3|:443... connected.
    HTTP request sent, awaiting response... 302 Found
    Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/511187726/5b2a5641-54d0-4dd0-a210-42bdc38235fa?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20220714%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220714T094850Z&X-Amz-Expires=300&X-Amz-Signature=8944cac2cd4ab82c300390b8ee5cb03b1b25e4d4d6900ba2c9299d38dda3d229&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=511187726&response-content-disposition=attachment%3B%20filename%3Dyolov7-e6e.pt&response-content-type=application%2Foctet-stream [following]
    --2022-07-14 09:48:50--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/511187726/5b2a5641-54d0-4dd0-a210-42bdc38235fa?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20220714%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220714T094850Z&X-Amz-Expires=300&X-Amz-Signature=8944cac2cd4ab82c300390b8ee5cb03b1b25e4d4d6900ba2c9299d38dda3d229&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=511187726&response-content-disposition=attachment%3B%20filename%3Dyolov7-e6e.pt&response-content-type=application%2Foctet-stream
    Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
    Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 304425133 (290M) [application/octet-stream]
    Saving to: ‘yolov7-e6e.pt’
    
    yolov7-e6e.pt       100%[===================>] 290.32M  34.8MB/s    in 8.5s    
    
    2022-07-14 09:48:59 (34.0 MB/s) - ‘yolov7-e6e.pt’ saved [304425133/304425133]
    


*At the time I’m writing those lines, YOLOv7 has just been released. Updates may occur and the weights may change, as well as the URL of their repository. If the link no longer works, check [this Github](https://github.com/wongkinyiu/yolov7) for the latest version.*

One last thing before using the template: upload your image!

**Either a single image, or several in a folder (YOLOv7 can handle several images at once).**

Feeling lazy ? You can simply upload our test image in one line of code :


```python
!wget https://raw.githubusercontent.com/tkeldenich/How_to_use_YOLOv7_Tutorial/main/man_cafe.jpg
```

    --2022-07-14 10:38:51--  https://raw.githubusercontent.com/tkeldenich/How_to_use_YOLOv7_Tutorial/main/man_cafe.jpg
    Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
    Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.108.133|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 47111 (46K) [image/jpeg]
    Saving to: ‘man_cafe.jpg.2’
    
    man_cafe.jpg.2      100%[===================>]  46.01K  --.-KB/s    in 0.007s  
    
    2022-07-14 10:38:52 (6.55 MB/s) - ‘man_cafe.jpg.2’ saved [47111/47111]
    


Let's see what it looks like:


```python
from PIL import Image
im = Image.open('man_cafe.jpg')
im
```




![png](Readme_files/Readme_15_0.png)



FINALLY, we can use YOLOv7!

To do this, we’ll call the detect.py file.

The python code in this file will run the detection for us.

**We only need to specify a few important parameters, in our case :**

*   weights we are using: `--weights yolov7-e6e`
*   image on which we want to apply the detection: `--source ./man_cafe.jpg`


```python
!python detect.py --weights yolov7-e6e.pt --source ./man_cafe.jpg
```

    Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.25, device='', exist_ok=False, img_size=640, iou_thres=0.45, name='exp', no_trace=False, nosave=False, project='runs/detect', save_conf=False, save_txt=False, source='./man_cafe.jpg', update=False, view_img=False, weights=['yolov7-e6e.pt'])
    YOLOR 🚀 v0.1-35-gef4dde4 torch 1.11.0+cu102 CPU
    
    Fusing layers... 
    Model Summary: 792 layers, 151687420 parameters, 817020 gradients
     Convert model to Traced-model... 
     traced_script_module saved! 
     model is traced! 
    
    /usr/local/lib/python3.7/dist-packages/torch/functional.py:568: UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument. (Triggered internally at  ../aten/src/ATen/native/TensorShape.cpp:2228.)
      return _VF.meshgrid(tensors, **kwargs)  # type: ignore[attr-defined]
     The image with the result is saved in: runs/detect/exp/man_cafe.jpg
    Done. (9.925s)


If you use your own image or folder, just change this last part to `./your_path`.

## **Understand the results**

**You'll find the detection output in the folder** `yolov7/runs/detect/exp`

*Carefull, if you run several experimentation, a new expN folder will be created. For your second experimentation it will be exp2. For the third, exp3, etc.* 

Here is our result :


```python
im_res1 = Image.open('./runs/detect/exp/man_cafe.jpg')
im_res1
```




![png](Readme_files/Readme_21_0.png)



First of all, we can see that YOLOv7 has a very good detection capacity. It even detects the person right behind our main character.

**You can see that it even indicates the confidence with which it detects objects/people. Most obvious objects are detected with a high confidence threshold. Comparing with [YOLOv6](https://inside-machinelearning.com/en/use-yolov6/) it detect every object on the first plan: two laptop, cellphone, book, cup. On this image, YOLOv7 is really amazing!**

So right now we have the default confidence threshold of 0.25. It means that every detection under the confidence threshold of 25% will be remove.

> The confidence threshold defines the minimum confidence value at which detection must be kept.

What if we wanted to increase this threshold?

**Actually it’s possible when running YOLOv7.**

Remember that we have defined some parameters. The mandatory parameters are the weights and the source (image path), but there are also default parameters that you can change to suit your needs.

**There are other parameters, for example:**

*   Confidence threshold: conf-thres (default value: 0.25)
*   Intersection over Union threshold: iou-thres (default value: 0.45)

Let’s change the confidence threshold to 0.6 :


```python
!python detect.py --weights yolov7-e6e.pt --conf 0.60 --img-size 640 --source ./man_cafe.jpg
```

    Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.6, device='', exist_ok=False, img_size=640, iou_thres=0.45, name='exp', no_trace=False, nosave=False, project='runs/detect', save_conf=False, save_txt=False, source='./man_cafe.jpg', update=False, view_img=False, weights=['yolov7-e6e.pt'])
    YOLOR 🚀 v0.1-35-gef4dde4 torch 1.11.0+cu102 CPU
    
    Fusing layers... 
    Model Summary: 792 layers, 151687420 parameters, 817020 gradients
     Convert model to Traced-model... 
     traced_script_module saved! 
     model is traced! 
    
    /usr/local/lib/python3.7/dist-packages/torch/functional.py:568: UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument. (Triggered internally at  ../aten/src/ATen/native/TensorShape.cpp:2228.)
      return _VF.meshgrid(tensors, **kwargs)  # type: ignore[attr-defined]
     The image with the result is saved in: runs/detect/exp2/man_cafe.jpg
    Done. (9.696s)


Result :


```python
im_res2 = Image.open('./runs/detect/exp2/man_cafe.jpg')
im_res2
```




![png](Readme_files/Readme_25_0.png)



Here we see that the book hasn't been kept.

Use YOLOv7, make assumptions for your project and set the confidence threshold that suits your need 😉

## **Changing weights**

Now you understand a bit more what YOLOv7 is.

Let’s go deeper.

There are different versions of YOLOv7 weights.

We have used a large version of these weights.

Large weights mean three things compared to the other versions:

1.   Better results (or at least a better understanding of the complexity)
2.   Slower computation speed
3.   More memory space used

**But what if you have space and time constraints?**

Well, ou can use other versions of these weights:

*   **Small**: https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
*   **Medium**: https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7.pt
*   **Large**: https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-e6e.pt

Again, you can download them manually [here](https://github.com/wongkinyiu/yolov7/releases) and then put them into your folder, or use `wget` and specify the version you want:


```python
!wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
```

    --2022-07-14 09:50:25--  https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
    Resolving github.com (github.com)... 140.82.113.3
    Connecting to github.com (github.com)|140.82.113.3|:443... connected.
    HTTP request sent, awaiting response... 302 Found
    Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/511187726/ba7d01ee-125a-4134-8864-fa1abcbf94d5?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20220714%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220714T095026Z&X-Amz-Expires=300&X-Amz-Signature=e32ddc97007a777e63e0656da05076f063107808aa2871462e14eb2e85923661&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=511187726&response-content-disposition=attachment%3B%20filename%3Dyolov7-tiny.pt&response-content-type=application%2Foctet-stream [following]
    --2022-07-14 09:50:26--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/511187726/ba7d01ee-125a-4134-8864-fa1abcbf94d5?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20220714%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20220714T095026Z&X-Amz-Expires=300&X-Amz-Signature=e32ddc97007a777e63e0656da05076f063107808aa2871462e14eb2e85923661&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=511187726&response-content-disposition=attachment%3B%20filename%3Dyolov7-tiny.pt&response-content-type=application%2Foctet-stream
    Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
    Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 12639769 (12M) [application/octet-stream]
    Saving to: ‘yolov7-tiny.pt’
    
    yolov7-tiny.pt      100%[===================>]  12.05M  10.8MB/s    in 1.1s    
    
    2022-07-14 09:50:27 (10.8 MB/s) - ‘yolov7-tiny.pt’ saved [12639769/12639769]
    


Depending on the weight version you’ve chosen, you will have :

*   **Small**: yolov7-tiny.pt
*   **Medium**: yolov7.pt
*   **Large**: yolov7-e6e.pt

To use it, replace `weight_file` here:


```python
!python detect.py --weights yolov7-tiny.pt --conf 0.25 --img-size 640 --source ./man_cafe.jpg
```

    Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.25, device='', exist_ok=False, img_size=640, iou_thres=0.45, name='exp', no_trace=False, nosave=False, project='runs/detect', save_conf=False, save_txt=False, source='./man_cafe.jpg', update=False, view_img=False, weights=['yolov7-tiny.pt'])
    YOLOR 🚀 v0.1-35-gef4dde4 torch 1.11.0+cu102 CPU
    
    Fusing layers... 
    Model Summary: 200 layers, 6219709 parameters, 229245 gradients
     Convert model to Traced-model... 
     traced_script_module saved! 
     model is traced! 
    
    /usr/local/lib/python3.7/dist-packages/torch/functional.py:568: UserWarning: torch.meshgrid: in an upcoming release, it will be required to pass the indexing argument. (Triggered internally at  ../aten/src/ATen/native/TensorShape.cpp:2228.)
      return _VF.meshgrid(tensors, **kwargs)  # type: ignore[attr-defined]
     The image with the result is saved in: runs/detect/exp3/man_cafe.jpg
    Done. (0.277s)


Result:


```python
im_res3 = Image.open('./runs/detect/exp3/man_cafe.jpg')
im_res3
```




![png](Readme_files/Readme_33_0.png)



**Now you know how to use YOLOv7!**

If you want to know more about [Computer Vision](https://inside-machinelearning.com/en/category/computer-vision-en/), feel free to check [our category dedicated to this topic.](https://inside-machinelearning.com/en/category/computer-vision-en/)

See you soon in a next post 😉
