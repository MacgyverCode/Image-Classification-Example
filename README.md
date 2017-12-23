
# Image-Classification-Example

Easy and Accurate Image Classification with Tensor Flow

### Brief Synopsis

In order to train the classifier we need to create a directory to house our images. In this example we create a directory in our root folder called training_images. In that directory we create subdirectories of all the image categories we want to train the model on. The training program will create labels from the names of the subdirectories and then train the model on the images provided.

We will also do our work from a pre-configured docker container in order to minimize development overhead.

## Download the Tensor Flow Docker Container
```bash
docker pull gcr.io/tensorflow/tensorflow:latest-devel
```

## Stand Up the Container
```bash
docker run -it -d gcr.io/tensorflow/tensorflow:latest-devel
```

## List Running Containers
```bash
docker ps -a
```

## Log Into Tensor Flow Container
```bash
docker exec -it _container_id_ bash
```

# From Within the Tensor Flow Docker Container Shell

Create a folder called "training_images" with subdirectories for each image category we want to include in our model.

```bash
mkdir training_images
```

Structure the folders like the following. The model will create labels from the names of the folders. So in this case there will be three categories: "pens", "laptops", "chairs". The names and file extensions of these images don't matter.
```bash
/training_images
   /pens
      image1.jpg
      image2.jpg
      ...
   /laptops
   /chairs
```

Copy this directory from our local machine into our docker container.

```bash
docker cp training_images _container_id_:/
```



## Training
This script will write both "retrained_labels.txt" and "retrained_graph.pb" this is our model. 

```bash
python tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/bottlenecks \
--model_dir=/inception \
--output_labels=/retrained_labels.txt \
--output_graph=/retrained_graph.pb \
--image_dir=/training_images/
```

## Prediction

We run a prediction and pass our trained model "retrained_graph.pb" along with out labels "retrained_labels.txt" as well as our novel test image "test-image.jpeg".

```bash
python tensorflow/tensorflow/examples/image_retraining/label_image.py \
--graph=/retrained_graph.pb \
--labels=/retrained_labels.txt \
--image=/test-image.jpeg 
```

# Push Model to Macgyver Marketplace

## Create a /macgyver Directory

```bash
mkdir macgyver
``` 

## Create a /macgyver/temp Directory

```bash
mkdir /temp/macgyver
```

## Create a Data file
This file will represent the client payload JSON when they hit our API.
```bash
cd /macgyver/temp
vim data.json
```

## Create Our main File
This file will run when a user requests this program from the API

```bash
vim main
```




























