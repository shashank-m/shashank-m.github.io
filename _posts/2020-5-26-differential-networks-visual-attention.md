# Differential networks and visual attention for fake news detection

Multimodal deep learning involves extracting features from different modes of data like text and images and combining these signals in an effective way to make a prediction. The part where features are combined is a challenging task and is not as straightforward as concatenating the features or doing a simple dot product of features obtained from the text and image.

There was a paper published in AAAI 2019 for Visual Question Answering which is also a multimodal task where a question is asked and we try to answer it by looking at both the image and question. Here they proposed replacing fully connected neural networks with something called differential networks.

What are differential networks?

![image](/assets/images/Screenshot 2020-05-26 at 2.27.25 PM.png)

Here, the pairwise difference of each element in the input vector is taken and this pairwise difference vector is multiplied with a weight just like in a Fully Connected network. Their hypothesis for differential networks is as follows:

Assume the image vector is v and text vector is q. They argue that doing a dot product between v and q is unreasonable as they probably do not belong to the same feature space. Instead they argue that vi -vj and ui - uj belong to the same space and a dot product of these differences would make more sense.

They also hypothesise that taking these differences can remove any noise present in the features. For example (vi+𝛅) -(vj+𝛅) will remove the noise present in these two elements.

Visual Attention:

![image](/assets/images/visual attention.png)

We pass the text through SBERT and the image through resnet 18. These two vectors are multiplied with a weight to get them down to the same dimension.

Next these two reshaped features are passed through a differential network respectively and their dot product is multiplied with a weight and softmax is applied along the first dimension to get 10 attention vectors of dimension 196 each as shown in the figure above.

Each of these 10 vectors is called an &#39;attention glimpse&#39; which look at different parts of the 196\*512 feature space as shown above. This is kind of similar to multi headed self attention in transformers where each head looks at different parts of the input sequence. It&#39;s just like an ensemble to explore more of the feature space.

SBERT

SBERT was chosen to extract features for the text. Why sbert? Why not just pass it through BERT and add up all the feature values of each word in the text?

That is because BERT on its own generates poor sentence embeddings. Using the output of the CLS token or adding up all vectors from the last self attention layer is bad practice which is proven in the sbert paper. The sbert paper showed that sentence embeddings from BERT&#39;s CLS tokens perform even worse than Glove embeddings. SBERT fine tunes BERT on Natural language inference tasks to improve sentence embedding quality.

Dataset:

The dataset consists of some news, the heading of that news article, an image and whether the news is fake or not. The above model uses only the heading and the image to make predictions. We achieved 0.9 train F1 and 0.87 val F1.

Future work:

Right now I&#39;m planning on exploring mechanisms like co attention which look at both the text and image while performing attention computations. Will also look forward to incorporating world knowledge using knowledge graphs.





