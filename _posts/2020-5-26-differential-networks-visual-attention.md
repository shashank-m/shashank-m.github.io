# Differential networks and visual attention for fake news detection

Multimodal deep learning involves extracting features from different modes of data like text and images and combining these signals in an effective way to make a prediction. The part where features are combined is a challenging task and is not as straightforward as concatenating the features or doing a simple dot product of features obtained from the text and image.

There was a paper published in AAAI 2019 for Visual Question Answering which is also a multimodal task where a question is asked and we try to answer it by looking at both the image and question. Here they proposed replacing fully connected neural networks with something called differential networks.

What are differential networks?

![image](/assets/images/Screenshot 2020-05-26 at 2.27.25 PM.png)

Here, the pairwise difference of each element in the input vector is taken and this pairwise difference vector is multiplied with a weight just like in a Fully Connected network. Their hypothesis for differential networks is as follows:

Assume the image vector is v and text vector is q. They argue that doing a dot product between v and q is unreasonable as they probably do not belong to the same feature space. Instead they argue that vi -vj and ui - uj belong to the same space and a dot product of these differences would make more sense.

They also hypothesise that taking these differences can remove any noise present in the features. For example (vi+𝛅) -(vj+𝛅) will remove the noise present in these two features.


