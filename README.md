# README

# Handwritten Digit Classifier from Scratch

A NumPy neural network that classifies 28×28 grayscale images
into digits from 0 to 9.

## What I implemented
- Forward propagation and backpropagation
- ReLU and softmax
- Mini-batch gradient descent
- Learning-rate reduction and early stopping
- Accuracy, cross-entropy loss, and macro F1

## Architecture
784 inputs → 10 hidden neurons → 10 output classes

##### - lowkey struggled a bit tryna match the dimensions for matrix multiplication

## Data preparation
Pixel values are divided by 255.
The data is split into training and validation sets.

## Results
Best validation loss: approximately 0.23.

## Heres What I learned:
In Machine Learning, when training an AI using the splitted data, in every epoch, the same data is used. Though this risks overfitting but it doesn't automatically cause it.

What I built was an MLP, a multi layer perceptron. This is specifically a shallow network because it only contains one hidden layer. Having multiple hidden layers turns it into a Deep Neural Network.

This network is a feed forward network. Pretty obvious ik ik  :>

Batching is taking the entire train test split and feeding it into the network while mini batches is taking small bite size peices of train test split and feeding it to the network.

Loss is basically the penalty. The lower it is, the better.

Precision basically says "out of all the images the network called (class_y), how many were really (class_y)? Used for minimizing the false alarms.

Recall as the word suggests, in a way its how well the model remembers. Out of all that really were (class_y), how many did the model find? Used for minimizing missed cases.

F1 score is the combination of precision and recall, its how well the model balances finding the right answers and voiding wrong guesses.

Macro F1 score is the average of the f1 scores of each class. (Note that each class have equal weights, meaning each class counts equally regardless of how many images it has).

Train Accuracy is not to be trusted and used as a basis for improvement. Best to use Validation Loss and Validation accuracy.

----------------------------------------------------------------------------
Xavier initialization chooses a starting weight scale that helps prevent signals and gradients from growing or shrinking repeatedly across layers, under suitable assumptions. Random sampling lets neurons start differently.
- Xavier uniform samples weights between −a and +a. These boundaries are symmetric around zero, but the sampled weights are not guaranteed to contain equal numbers of positive and negative values.

- ReLU changes negative weighted sums to zero. For roughly symmetric, zero-centered weighted sums, this removes about half of their average squared signal. Repeating that reduction across many layers can make signals very small.

Kaiming initialization chooses a larger weight variance to compensate for this reduction. For equal-width layers, standard Kaiming weights have √2 times the standard deviation of standard Xavier weights. This doubles the weight variance, helping maintain signal size through ReLU layers under the initialization assumptions.

- Kaiming normal samples from a zero-centered bell curve. Large magnitudes are possible but rare. Kaiming uniform uses fixed boundaries instead.

Neither method guarantees that gradients will remain well behaved throughout training.


• With Xavier + ReLU: By the time you get to a 50-layer deep network, your signal variance is practically zero (0.5⁵⁰). The network can't learn because the activations vanish.
• The Kaiming Fix: Kaiming multiplies the weights by \(\sqrt{2}\). This effectively doubles the variance at each layer, exactly compensating for the 50% loss caused by ReLU. It keeps the network alive on step zero.

----------------------------------------------------------------------------
    
How gradients update weights, how to evaluate a classifier,
and how to debug an inactive ReLU layer.

## Other concepts I applied

**Input normalization:** I divided pixel values by 255 to change their range from 0–255 to 0–1. This preserves the image shades while controlling the input scale.

**Matrix operations and vectorization:** I represented images as columns and processed multiple images with matrix multiplication, instead of calculating each neuron and image separately.

**Biases:** Each neuron has a learned offset added to its weighted sum. This lets the neuron shift its activation point.

**Activation functions:** ReLU introduces a nonlinear operation between weight layers. Without it, my two weight layers would be equivalent to one linear transformation.

**Softmax and argmax:** Softmax converts output scores into probabilities that sum to 1 for each image. Argmax selects the class with the largest probability.

**Cross-entropy loss:** I penalized the model based on the probability it assigned to the correct class. A higher correct-class probability produces a lower loss.

**Backpropagation and the chain rule:** I calculated how the loss changes with each weight and bias by working backward through the network. The chain rule connects these changes across layers.

**Mini-batch gradient descent:** I averaged gradient contributions across each training batch, then updated the weights and biases once per batch.

**Learning rate:** This controls how strongly each gradient changes a parameter. It multiplies the gradient; it is not the full update size by itself.

**Validation:** I measured performance on separate images without updating weights. This helped guide training decisions.

**Whole-epoch metrics:** I accumulated correct counts, image counts, and loss sums across batches. I then calculated metrics for the whole dataset pass.

**Confusion matrix:** I counted actual–predicted class pairs to identify which digits the model confused. I also used those counts to calculate per-class F1.

**Learning-rate reduction on a plateau:** When validation loss stopped improving for several epochs, I reduced the learning rate to allow smaller updates.

**Early stopping and patience:** I allowed several epochs without improvement before taking action. After the permitted learning-rate reductions, further stalling stopped training.

**Best-model checkpointing:** I saved copies of weights and biases whenever validation loss reached a new best value. At the end, I restored that checkpoint.

**Numerical stability:** I subtracted the largest score before calculating softmax exponentials to prevent overflow. I clipped probabilities before taking logarithms to avoid log(0).

**Debugging with measurements:** I inspected gradient sizes, the learning rate, and the fraction of positive hidden activations to investigate stalled learning.

**Reproducible initialization:** I used a random seed so I could reproduce the same initial weights.




This neural network was one heck of a y = mx + b, with a few bends and a lot of adjustable knobs.