# Cancer-classification-TCGA

Deep Learning Based Tumor Type Classification Using Gene Expression Data


In the field of bioinformatics, Deep learning and CNNs are widely used. As an
example, for tumor type classification CNNs are applied to gene expression
data. But firstly, the gene expression data are transformed into images and then
CNN is applied. On genomics data, Tumor type classification can contribute to
a faster and more accurate diagnosis. However, tumor type classification using
genomics data is currently infrequent. It is because of the difficulty with the
high dimensionality of the genomic dataset . A large volume of tumor tissues
has been sequenced and managed by The Cancer Genome Atlas (TCGA) for
better understanding of the cause of these tumors. For 33 most prevalent forms
of cancer, TCGA analyzed over 11,000 tumors which led to the development
of the Pan-Cancer Atlas Database. Each tumor sample, we could access its
RNA-Sequence expression data. We could identify potential biomarkers for
each tumor while using this data. The Pan-Cancer Atlas provides a plethora of
information on these 33 tumor types. The Pan-Cancer Atlas contains
information for more than 20k genes about their normalized mRNA-seq gene
expression data. A lot of these genes have no specific effects on the tumor,
hence they are known as weak genes.

Data

Normalized-level3 RNA-Seq gene expression data of
33 tumor types in Pan-Cancer Atlas is used. There were 20531 genes per
each patient. To input the data to the convolutional neural network, we
embedded the data into 2-D images. The data contains 10332 tumor samples
for 20531 genes.

Preprocessing

The data contains the normalized read count for each gene, but the range of
the values is huge, and also some values are smaller than 1. So, Firstly a
transform using log2( x + 1) is applied to reduce the scale. Then the genes for
which the value is NA for any patient are dropped. Then a threshold of
variance equals 1.19 is used to filter out the genes with small variance across
all the samples. And the number of genes is further reduced to 8171. This
threshold was chosen carefully. A higher threshold reduces more weak
features so that the classification accuracy can be improved and a lower
threshold can retain more genes so that the real gene-specific biomarkers
will not be missed. Then, we embedded the high-dimension expression data
(8464 x1) into a 2-D image (92x92) by adding some zeros at the last line of
the image to fit for the convolutional layers. Next, we constructed a
three-layer convolution neural network and used 10-fold cross-validation to
test the performance.

Classification

A three-layer convolution neural network is built. In conclusion, a
convolutional neural network consisting of three convolutional layers, and
three fully-connected layers. The initial convolutional layer contains 64
different filters, while the second and the third convolutional layers contain
128 and 256 filters respectively. Padding was also done. The
Batch-normalization layer including the Max-pooling layer is followed
directly after each convolutional layer. The activation function executed
with conv2d layers is “relu”. A drop-out layer is added before starting into a
fully connected layer, the drop-out rate is 25%. The measurements of the
three fully connected layers are 30976, 1024, 512 individually. “Categorical
Cross Entropy” as loss function and Adam optimizer to update the weights
were used. The learning rate is “1.0e-4”. 10-fold cross-validation is used to
train the convolutional neural network and to examine the performance.
