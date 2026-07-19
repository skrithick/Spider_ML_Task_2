# My Observations and Understanding of Transformers vs. LSTM

**(These are comparosons for the *non-normalized values, in celcius*)**

>*Note: The transformer and lstm here both are trained on previous 72 hours and predict next 12 hours. This has been done so that a fair comparison can be made. But I got a good result even for the transformer's 720 input hours and 24 output, that code has also been attached*

| Type of Loss | LSTM | Transformer |
| --- | --- | --- |
| Huber | 0.8296 | 0.8288 |
| MSE | 2.8131 | 2.7695 |
| MAE | 1.2264 | 1.2282 |

*We can see that the transformer yielded slightly better results.*

- LSTM: `hidden_size=128, 1 layer`
- Transformer: `64 model dim, 4 heads, 3 layers`

- In terms of the prediction quality, it's evident from the graphs that the transformer performs slightly better. I also believe that with more input data, (maybe if not downsampled), the transformer could've had a chance to show it's true capabilities. I'd actually planned to test that too.

- Also with a large number of input data or sequences, the transformer definitely works better. This is coz the transformer uses attention with different heads to compute the relationship between every piece of input data. Because of this even a random input sequence at the end can learn from one at the beginning.

- When it comes to lstm, the understanding of data occurs sequentially, piece-by-piece so during backprop, the weightage of earlier data might be lose.

- In terms of speed, I found that the transformer ran way faster than the lstm (The lstm speed could've increased if I used the native nn.LSTM but I doubt it would exceed the transformer), especially with the same split. Upon researching I found out that lstms work sequentially, in order for it to parse say, the 10th piece in a sequence, it has to have parsed sequences 1-9. But in a transformer, because of the attention sequence, it analyses all the data pieces simultaniously, understanding the relation between them in terms of different cases with the heads. So because of this parallel running, transformers generally have less runtime as compared to lstms.

- However, though they might be fast, transformers need a lot more memory. An LSTM needs to store only an additional element to the hidden state and a processed cell state. A transformer needs to simultaneously store the relation parallely, between all data points so it needs more memory.

- I had mentioned in the lstm notes that they were made to fix the issue of gradients going to 0 in after deep processing through rnns. Transformers don't face this issue as they map the relation between 2 points, so there's no deep sequence to lose gradients to.

- But I strongly believe that a LSTMs can stil be relevant (I'm not sure about the real world metrics but). This is as the transformer has no sequential knowledge. It can map the relation between the different pieces of data and understand the dependancy of one on the other but it lacks the memory that this data comes after this one and so on. **(This is only for a vanilla transformer but with positional encoding, this can be fixed)**. Also lstms need much less computing power as compared to the transformer, which makes them suitable for faster, lighter tasks. One major reason is that a transformer performs best with a large amount of input data. For forecasting tasks with a lesser amount of data, an LSTM can be used.

![alt text](plots/transformer_vs_lstm.png)

- So for this task, the loss for the transformer was slightly lower than the LSTM and the predictions graph is a bit more accurate as well. In fact, the transformer gave good results even for 720 input hours and 24 output hours. This just goes to show the extent of memory power of the transformer.

*A huge thanks to my spider seniors and my mentor, Rishabh*