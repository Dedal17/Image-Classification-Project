# Image-Classification-ProjectData set: 
Link to the data set https://stanfordmlgroup.github.io/competitions/mura/
MURA consists of images 7 types: hand, humerus, forearm, finger, wrist, elbow, shoulder. The purpose is to build a model that classifies images as negative ('healthy' - 0) or positive('abnormal' - 1). There is a 'train' set and a 'valid' set (used actually for testing) inside the archive. Note that the total data is very large (approx 3 GB)

Data extraction:
Using a separate scipt I've split images based on their kind. In folders 'train_specific_paths' and 'valid_specific_paths' one can find .csv files which contain the necessary paths used to extract data.
Here, use the functions extract_data (to extract specific kind of images; ex: 'elbow') and extract_all_data. These functions return a 4-tuple: np arrays representation of train images, labels of train images, test images, labels of test images.
Note that when calling extract_data or extract_all_data, the first parameter is the path to the location of MURA (so if needed, please change 'D:\\python' in order to make the example work)

Model:

Given the task is image classification, the model proposed is a convolutional neural network (CNN). Below one can find my reasoning for the design decisions made.

Preprocessing: MURA images are either RGB or greyscale. Because of the nature of classification, converting them to greyscale is preferable. Images have different shapes, I chose to reshape all of them to (512,512), because 512 is the maximum value their shaes can take and so no information will be lost.

Choosing the right parameters: using k_fold_cross_validation (k = 5) and classic_validation functions I computed the values to be used for the 2 pairs of convoltuion layers + maxpooling and the size of the fully connected dense layer. 3 different types of models have been trained, the one selected was the one with better accuracy on the test set.
Accuracy of the presented model: 61% on test set 

Metrics used: accuracy and confusion matrix (see conf_matrix function)
Dealing with overfitting: because of the large size of the train set, overfitting can be an issue. I've added dropout layers (of small values for the conv layers: 0.2 and 0.5 for the dense layer) and mainted a validation set (in classic_validation 20% of train data is saved for validation)

Limitations:The large size of the data set, makes training models take a very long time ( approx. 5 hours to train a model on elbow images alone) and so more experimenting is required in order to improve the model.
