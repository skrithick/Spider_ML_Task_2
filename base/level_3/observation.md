# Discussion about the workings of transformers

- Attention for sequence modelling:
    - Transformers don't need to shove an entire big sequence of data into memory, instead they look at specific parts of the data, map their relation using self attention with different heads, they can understand which parts of the data are actually relevant.
    
    - Also even with really large sequences of data, attention is calculated for every part of the data and the important bits are identified.

    - Right now I did forecasting but in tasks like text processing, words can have different meanings depending on the context. Self attention allows the transformer to understand the context, and map the relation regardless of where the word might be used.

    - And as mentioned in the comparison, attention uses parallel processing which makes the transformer speedy.

- Recurrence vs. Attention is something very close to the heart of transformers, and I've used it to answer almost all questions pertaining to the performance of transformers. Recurrence is when each piece of the input data is processed sequentially, step-by-step to build memory. The issue is that with large sequences, the context of earlier sequences can be lost. Attention on the other hand is when all the data is processed simultaneously and the relation between different parts of the data is found, and the different types of relations depend on the heads.

- I've included an analysis of situations in which LSTMs are still useful in the comparison, this is just yanked from that:
    > But I strongly believe that a LSTMs can stil be relevant (I'm not sure about the real world metrics but). This is as the transformer has no sequential knowledge. It can map the relation between the different pieces of data and understand the dependancy of one on the other but it lacks the memory that this data comes after this one and so on. **(This is only for a vanilla transformer but with positional encoding, this can be fixed)**. Also lstms need much less computing power as compared to the transformer, which makes them suitable for faster, lighter tasks. One major reason is that a transformer performs best with a large amount of input data. For forecasting tasks with a lesser amount of data, an LSTM can be used.

- Transformers however definitely perform better when there's complex input data with complex relations between them, especially when the input sequences or the size of the data is large. Both in terms of speed and performance. Transformers ensure that context from earlier sequences are not lost, that the relation between different parts of the sequences are maintained and that all data is properly utilized. Hence even today, to my knowledge transformers are used everywhere, literally EVERYWHERE, and I find that to be really cool.