Video Classification with a CNN-RNN Architecture
================================================

This code is not our own, it is attributed to Sayak Paul and Keras.
Accessed from: https://keras.io/examples/vision/video\_classification/

This program is a video classifier that uses a hybrid architecture
consisting of a convolutional neural network and recurrent neural
network. Convolutional neural networks are robust in their ability to
recognize and classify images. Using a CNN as well as a recurrent neural
network allows this program to handle sequential data and memorize
previous inputs. This hybrid architecture can process videos well as the
input it is given is simply a collection of a set of images arranged in
a certain order or an ordered sequence of frames (a video!). Each frame
contains spatial information meaning that takes up some space and
temporal which infers that it has some information related to time.
Convolutional neural networks have been used to develop some of the best
image recognition algorithms. Therefore, since there exist "images" in
videos a convolutional neural network will be ideal for processing the
spatial information. Recurrent neural networks come into play as they
act as incorporating their layers' work to process temporal information.
This sort of system is known as a CNN-RNN hybrid and such architecture
is used to build our video classifier.

The data set used to train and test our network is taken from the UCF101 dataset and has been used to
build other networks capable of action recognition. TensorFlow and
TensorFlow Docs were used in our network. Lastly, GRU layers are used in
the network. Using the !wget command the files containing the dataset
were retrieved and extracted using the !tar xf command. 

During data preparation, the input data (videos) is standardized before being fed to
the neural network. Each video is cropped around its centre, and its
frames are captured at a fixed interval until the maximum number of
frames is reached. This program uses a pre-trained model to extract
meaningful features from the data. The labels of the videos in strings
are encoded to integers. 

After the data has been prepared, it is fed
into the sequence model. Since we are using a recurrent neural network
that uses sequence data, we use masking to indicate to layers that not
all time-stamps for a video are present (since we captured frames at
intervals, not all frames). 

The Inference section is where we sample a
random video from our test data by outputting the network's predictions
for the video's classification. The prepare\_single\_video() function
works synonymous to the prepare\_all\_video() function as it takes in
extracted frames as parameters and then converts the frames into a form
that is feedable into the sequence model. Part of its functionality
involves implementing a feature extraction model that uses a CNN
architecture to get from the frame's important features. The function
returns the features as a multidimensional array (1xMaximum Sequence
Length x Number of Extracted Features) as well as an multidimensional
array frame\_mask that determines in the timestep has been masked with
zeros due to the length of the video being shorter than the maximum
sequence length. 

The sequence\_prediction() is the function that
actually feeds our sample video into the network and then prints out the
probabilities i.e., classifies the video. It's input parameter is a
video file and the function is an RNN implementation of the system. The
function calls the prepare\_single\_video() so that it can convert the
given video file into the multidimensional array of extracted features
into a sequence model. The sequence model is the final classifier that
predicts probabilities of the actions in the video. These probabilities
are then printed out as a percentage along with the text label of each
predicted action of the video. The last function represented in this
section is the to\_gif() function that also takes in the frames of a
video and converts it to a gif file embedded into the program. This is
used for visualization.

Lastly, a call to all the functions described is
made resulting in a printout of the systems prediction of the
classification of the video and a visualization of the classified video
embedded in the program in the form of a gif. The output of this program
is percentages for each possible video indicating the likelihood that
the given test video matches it. We interpret the video with the highest
percentage to be the video that is most likely the given test video.
