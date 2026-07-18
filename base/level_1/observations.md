# My observations from resnet

- The main thing I first learned was that, intuitively it's easier for the model to predict changes and deltas rather than the final output. It increased performance as the model already had a base to work on, and it reduced the load on the model a lot, and made it faster too.

- Also, since resnets have complex connections and archs, during backprop, their gradients get multiplied by so many matrices with weights less than one, they might tend to 0.

- Even during forward processes, the input signal is lost when deeeep architectures are used. So, residual connections help by preserving different checkpoints of data input so that the model doesn't get lost further down in the architecture.

- Also if the model predicts `x + f(x)` (f(x) is after the batch norm and relu and stuff), then when we differentiate, we get `1 + f'(x)` which means that the gradient is a bit safer due to the +1 term. (To my understanding)

- One important thing I learnt was about the importance of batch norming in resnets. The skip connections help the gradients, but they would be unstable without batch norm. Coz if we don't norm, the scale of the original x and the new f(x) we're adding might be completely different, so it's important to normalize.

- Also if the layer doesn't predict properly it can just output 0, saving the rest of the model as the gradient is still 1. If this wasn't there the gradient would be 0 and the model would stop learning after that point. It would be a zombie neuron.

- I tried with both resnet-18 and resnet-20 and resnet-18 performed slightly better. I think this is because although resnet-18 has less layers, it has more parameters which give the model more thinking capability. If the architecture is too deep it should have better capabilities, however, I noticed that overfitting can occur.

# Challenges Encountered:

- Learning took a while, coz initially, in my mind I had confused that stride and pooling were interlinked. But after a while I realized that we weren't pooling. Building a mental image of what I'm doing, and envisioning the images, pixels took some time too. But my notes helped a LOT.

- Deciding the architecture: There were so many different kinds of resnet architectures available, I tried them all but found that I didn't like completely overpowered models with a ton of parameters. I liked resnet 18. _I also tried my own architectures too, changing the funneling, dimensions, etc. and reached a point I felt satisfied with._

- Not exactly a challenge, but when I was using transforms, some of the libraries were deprecated but still worked, I've got to update myself.

# Some more stuff

- As I was building the transformer for level 3, I noticed that we used residual connections there too, a sort of mini resnet. So I wanted to find out how resnets were used inside transformers.

- After the attention was calculated and passed through the ff networks, the original input vector is added to the calculated output. Again, this helps in gradient safety during backprop, and allows for the original input information weight to not get lost. It's also faster and more intuitive for the model to have less to predict.

*A huge thanks to my spider seniors and my mentor, Rishabh*