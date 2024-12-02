# thoughtCode

EEG headset -> instructions and codegen

This would need people to read text and code while wearing an EEG headset, and it cant really be more than 60s, and will have lots of noise(might help if they read the data out loud, Cerebellum + Broca's area stimulation)

Hard to scale the data to the size of anything like an LLM, paragraphs will be 200 words at most, need like 30-40 humans to eliminate noise and generalize, so for a goodish LLM, need like 1B tokens, or 730m tokens, about 18m english words on per person for 40 people, which is impossible. 

We can maybe get 3 paragraphs per person, gives us around ~600 words per person, which would easily overfit any kind of decoding process

we could Use RNNs, which can [generalize okayishly (see wikipedia ex.)](https://karpathy.github.io/2015/05/21/rnn-effectiveness/), in 100mb, which is like 100m chars, and 200 words is ~1200 chars, or 1w 6c, so we could train the model on 16m words total, or about 400,000 words per person if 40 people. 

if we adapt techniques from medical domains, where RNNs perform very well on stuff as low as 2000-10000 samples, we can probably shrink this task down to 100 people, each person reading 5 different paragraphs, but each paragraph being read by 10 people, or about 50 paragraphs, 200 words, or about 10000 words, 60000 chars, and if outputs are still weak at this point, we can use a seq-to-seq transformer between the outputs and actual text read by people

from here we give the text to an LLM, Llama-3.1-7b (larger probably makes sense, but a model this small can make tokens rather fast in low hardware settings, so a EEG headset+laptop setup could work in semi-realtime), and have it generate the code.

## logic puzzles: a Neuralink PoC

A common example is the [Chimp memory puzzle](https://www.youtube.com/watch?v=PNrWUS13th8), we can expand this by model a couple more series (slices from 1-20, ex. 1-5, 9-18, etc, only odds, only evens fibbonacci, increasing order), training each chimp on 5 or less puzzles, and with neuralink having far less noise than EEGs, we can have 2-3 chimps per puzzle, and with lots of random grids, we can make 10k datapoints in ~10 chimps, represent initial state as a grid, and final state as the actual series. 







