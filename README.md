
# Image-Classification-Example

Easy and Accurate Image Classification with Tensor Flow

### Brief Synopsis

In order to train the classifier we need to create a directory to house our images. In this example we create a directory in our root folder called training_images. In that directory we create subdirectories of all the image categories we want to train the model on. The training program will create labels from the names of the subdirectories and then train the model on the images provided.


## Download the Tensor Flow Docker Container
docker pull gcr.io/tensorflow/tensorflow:latest-devel

## Stand Up the Container
docker run -it -d gcr.io/tensorflow/tensorflow:latest-devel

## List Running Containers
docker ps -a

## Log Into Tensor Flow Container
docker exec -it _container_id_ bash


# From Within the Tensor Flow Docker Container Shell

## Training
```bash
python tensorflow/tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/bottlenecks \
--model_dir=/inception \
--output_labels=/retrained_labels.txt \
--output_graph=/retrained_graph.pb \
--image_dir=/training_images/
```

## Prediction

python tensorflow/tensorflow/examples/image_retraining/label_image.py \
--graph=/retrained_graph.pb \
--labels=/retrained_labels.txt \
--image=/test-image.jpeg 











