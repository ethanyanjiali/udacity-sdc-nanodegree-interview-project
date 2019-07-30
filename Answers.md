I choose the Deep Learning Engineer role
> Explain a recent project you've worked on. Why did you choose this project? What difficulties did you run into this project that you did not expect, and how did you solve them?

One of the recent project I've been working on is to train a hand classification model to determine if we should trigger a hand AR effect in the app. The most difficult problem for us is the dataset. Because we try to understand user intent, sometimes it's not quite clear if an image should be labeled as true of false. And this makes it harder for us to communicate with labelers. We solve them by converting the classification task to a bounding box task, so that we can later filter the labeled dataset based on the area of the bounding box. Another chanllenge is the unbalance data, it's relative easy to define positive data for hand classification, but there're way more negative examples required to make the model robust enough. We made a iterative model improvement pipeline to keep collecting negative examples for our model training to solve this problem.

> How do you deal with severely unbalanced data? In what situations might this occur?

There're multiple weights to deal with severely unbalanced data.
1) We could collect more data for the minority category if possible.
2) We could use weighted loss function, such as weighted cross entrophy.
3) We could upsample those lesser categories and undersample those more prominent cateogies

This could occur when one of the category is hard to collect, for example, in Open Images dataset, since most of the images are from Internet, there're lots more Person(879617) and Tree(441345) images than Grinder(101) and Paper Cutter (95). Another possible scenario for unbalanced dataset is the binary classification, where sometimes postive or negatives examples are much more likely to happen than the other. For example, a dataset for certain rare disease, it's much harder to collect positive examples.

> What is the difference between object classification and detection? How do any related architectures often differ to accomplish these tasks?

Object classification tells what categories the object belong to, while the detection gives a bounding box to locate the object. Networks used for Object classificaiton are ResNet, VGG, GoogLeNet, etc. Networks used for Object detection are YOLO, SSD, Faster-RCNN. Usually, a detection architecture will use a classificaiton architecture as a backbone network. Some of the detection models, such as Faster R-CNN, use a technique called Region Proposal to find the region of interest first then classify over that region. However, some other detection models, such as YOLO, don't rely on regions, but splits the images into grids before classification.

> [Code] Explain a recent deep learning research paper you read and how it improved upon existing methods. What were its strengths and weaknesses? Code a mock-up of the network used in this paper in your desired deep learning library.

I read a paper called "Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks" which proposed a network called CycleGAN. Before CycleGAN, most of the image translation tasks were done by auto encoders or GAN with small hand crafted dataset. However, one problem is that it's really hard to annotate dataset for image translation. For example, to convert a Van Goh work to Monet work, it's impossible to have Monet to draw all Van Goh's painting so that we can collect training data. CycleGAN invented a cyclic loss so that we can train a GAN using unpaired dataset. It demonstrates its ability by converting a horse image to a zebra image while still preserving the background and other unrelated objects.

I have coded this network in code.py in this repo using TF 2. I didn't use C++ because it's mostly implemented with Python.

