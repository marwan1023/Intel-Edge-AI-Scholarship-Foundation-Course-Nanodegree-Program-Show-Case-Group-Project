# Intel-Edge-AI-Scholarship-Foundation-Course-Nanodegree-Program-Show-Case-Group-Project

Participation in the Intel Edge AI Udacity Scholarship Show Case Group Project  
* Follow Udacity Git Commit Message Style Guide: https://udacity.github.io/git-styleguide/     

[image1]: ./images/ModelOptimizerFlow.png    
[image2]: ./images/TensorFlowObjectCountingAPI.jpg 
[image3]: ./images/VideoTrackingFlow.png 
[image4]: ./images/SSDWithMobilenet.png
[image5]: ./images/result.gif
[image6]: ./images/Flow.png
[image7]: ./images/resultInTaipeiCity.gif
[image8]: ./images/TaipeiOutput.gif
[image9]: ./images/output.gif
[image10]: ./images/IndiaOutput.gif
[image11]: ./images/indoutput.gif

Collaborators:  

| Name | Slack Name |
| ------------------------- | ------------------------- |
| [Sarah Majors](https://github.com/sfmajors373) | Sarah Majors | 
| [Harkirat Singh](https://github.com/Harkirat155) | Harkirat |
| [Hsin Wen Chang](https://github.com/Polarbeargo) | Bearbear |
| [Halwai Aftab Hasan](https://github.com/ahkhalwai) | aftab |
| [Anshu Trivedi](https://github.com/AnshuTrivedi) | Anshu Trivedi |
| [Frida Rode](https://github.com/fridarode) | Frida |

Our story start from trying to mitigation traffic jam in every city globally. In the early stage perform statistics inference detected objects on the video stream to inform traffic status in real-time. In this Intel® Edge AI Group showcase project, our goal is to extend our learning experience from Intel® Edge AI Scholarship Foundation Course Nanodegree and Hands-on Implementation as follow:    
* Import OpenVINO Toolkit, build and compile successfully on Google Colab.  
* Load pre-trained models.  
* Perform model optimization.  
* Integrate with TensorFlow Object Counting(TOC) API, the TOC API is the object detection implementation that runs and infers using the TensorFlow models at the backend; and is optimized to run at the edge using OpenVINO toolkit from Intel.  
* Perform statistics inference detected objects on video stream.

## Load Pre-trained Models   

*  You can use public or pre-trained models. To download the pre-trained models, use the Tensorflow Model Downloader or go to [PreTrain Model Download](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz)
* Before running the demo with a trained model, make sure the model is converted to the Inference Engine format (*.xml + *.bin) using [The Model Optimizer](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html)

## The Intel OpenVINO Toolkit Model Optimizer Flow Chart 
 In this project, we feed the model into the Model Optimizer, and get the Intermediate Representation. The frozen models will need TensorFlow-specific parameters like `--tensorflow_use_custom_operations_config` and `--tensorflow_object_detection_api_pipeline_config`. Also, `--reverse_input_channels` is usually needed, as TF model zoo models are trained on RGB images, while OpenCV usually loads as BGR. Certain models, like YOLO, DeepSpeech, and more, have their own separate pages.  
 
![][image1]  
### Quantization

* Quantization is the process of reducing the precision of a model. In the deep learning research field, the predominant numerical format used for research and for deployment has so far been 32-bit floating point, or FP32. However, the desire for reduced bandwidth and computational energy consumption of deep learning models has driven research into using lower-precision numerical formats. It has been extensively demonstrated that weights and activations can be represented using INT8 without incurring significant loss in accuracy. The use of even lower bit-widths, such as 4/2/1-bits, is an active field of research that has also shown great progress. 
* The OpenVINO™ Toolkit, models usually default to FP32, or 32-bit floating point values, while FP16 and INT8, for 16-bit floating point and 8-bit integer values, are also available (INT8 is only currently available in the Pre-Trained Models; the Model Optimizer does not currently support that level of precision). FP16 and INT8 will lose some accuracy, but the model will be smaller in memory and compute times faster. Therefore, quantization is a common method used for running models at the edge.

| INT8 Operation | Energy Saving vs FP32 | Area Saving vs FP32 |
| :---         |     :---:      |          ---: |
| Add   | 30x     | 116x    |
| Multiply     | 18.5x      | 27x      |  

---

### Supported Devices

The following Intel® hardware devices are supported for optimal performance with the OpenVINO™ Toolkit’s Inference Engine:
| Device Types  | 
| ------------- | 
| CPUs  | 
| GPUs  |
| VPUs  | 
| FPGAs|

---
## Integrate With TensorFlow Object Counting API  
--- 
***The [TensorFlow Object Counting API](https://github.com/ahmetozlu/tensorflow_object_counting_api) is used as a base for object counting on this project, more info can be found on this [repo](https://github.com/ahmetozlu/tensorflow_object_counting_api). And a modified version [repo](https://github.com/Polarbeargo/tensorflow_object_counting_api.git) for run on Google Colab***

---
### TensorFlow Object Counting API  Work Flow
In this section, we further enhance real-time object counting by using TensorFlow Object Counting API to process input video stream perform real-time object detetction, track and count.  
![][image6]
### System Architecture  
![][image2] 

### Object Tracking Flow Chart
In this section, we use what we learn from The Intel® Edge AI Scholarship Foundation Course Nanodegree Lesson 5 Deploying an edge app section 4 Handling Input Streams implement 'cv2.VideoCapture' lifecycle and 'cv2.VideoWriter' fulfilled Object Tracking and count detected Objects work flow.  

![][image3] 
### Model Architecture  
In here, we use the Single Shot Detector with MobileNet from [ TensorFlow Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md). SSD is designed for object detection in real-time. SSD speeds up the process by eliminating the need of the region proposal network. SSD applies multi-scale features and default boxes to recover the drop in accuracy. These improvements allow SSD to match the Faster R-CNN’s accuracy using lower resolution images thus pushes the speed higher.

![][image4] 
## Citation  

    @ONLINE{tfocapi,
        author = "Ahmet Özlü",
        title  = "TensorFlow Object Counting API",
        year   = "2018",
        url    = "https://github.com/ahmetozlu/tensorflow_object_counting_api"
    }

## License
This system is available under the GNU - 3.0 license. See the [LICENSE](https://github.com/Polarbeargo/Intel-Edge-AI-Scholarship-Foundation-Course-Nanodegree-Program-Show-Case-Group-Project/blob/master/LICENSE) file for more info.

## Perform Statistics Inference On Video Stream Results
The following is our current progress status to perform statistics inference on video stream. 

General Count                      | Multi class count
:-------------------------:|:-------------------------:
Barcelona
![][image5]                | ![][image9] |
Taipei City                     
![Result in Taipei City][image7] | ![Result in Taipei City][image8] |
India                     
![Result in India][image11] | ![Result in India][image10] |


## Future Work
In this project, we successfully perform statistics inference detected objects on the video stream to inform traffic status in real-time. The next step we will implement the part to detect car accident through surveillance camera systems and throw alert in real-time inform the need of to mitigation traffic route can be applicable in every city globally.  

# References

* [OpenVINO on Colab](https://github.com/alihussainia/OpenDevLibrary)  
* [OpenVino For SmartCity](https://github.com/incluit/OpenVino-For-SmartCity)  
* [TensorFlow Object Counting API - on Colab Version](https://github.com/Polarbeargo/tensorflow_object_counting_api.git)  
* [Udacity OpenVINO Exercise on Colab](https://colab.research.google.com/drive/1xla23daYYbTIfbdHF0nyHzHyoAvVtyaG#scrollTo=niqr_H0TD4Ie&forceEdit=true&sandboxMode=true)  
* [The Intel OpenVINO Toolkit Model Optimizer Flow Chart](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_Deep_Learning_Model_Optimizer_DevGuide.html)
* [Supported Devices](https://docs.openvinotoolkit.org/latest/_docs_IE_DG_supported_plugins_Supported_Devices.html)  
* [ TensorFlow Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)
* [MIT xPRO - Tackling the Challenges of Big Data](https://mitxpro.mit.edu/courses/course-v1:MITProfessionalX+6.BDX+T3_2016/about)
