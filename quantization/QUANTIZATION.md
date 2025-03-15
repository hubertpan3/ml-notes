#Quantization

Quantization is the action of reducing neural network based model sizes. (Also known as "model compression")
When it comes to neural network based models each neuron often has associated weights typically represented as 32 bit floating point numbers FP32.
When training these models in the raw form tweak these weights until a particular objective is met.
This means that models using FP32 weights will require 32 bits per weight parameter.

For example, 8 billion parameter llama3.1 8b model would require ~30 GB of space to hold all of the FP32 weights.

```
(8000000000 * 32)/8/1024/1024/1024 = 29.8023223877
```

However with 4 bit quantization, we can reduce the required space down to  ~4 GB.

```
(8000000000 * 4)/8/1024/1024/1024 = 3.725
```

This can be validated by looking at the 8b llama3.1 entry on ollama:
https://ollama.com/library/llama3.1 

## Mechanics of Quantitization
As noted in [1] Quantitization is the process of mapping the FP32 space into a smaller bit space.
This can be done by scaling the numbers into the smaller range and clumping them into discrete bins (if necessary). In my head this process is analogous to some of the more primitive image compression techniques where color ranges were restricted et.al.

Note, this scaling process doesn't have to be linear, if the weight values are unevenly distributed we can use clustering algorithms like k-means to determine how raw FP values are mapped to bins in the smaller bit space.

## Llama Quantization labels

Labels such as "Q4_K_M" follow the convention of:
 - `Q` stands for Quantization
 - `4` the number of bits used in the quantization process
 - `K` means that k-means clustering was used in the quantization process
 - `M` indicates the "size" of the model post quantization
  - common values include (S -> Small, M -> Medium -> L -> Large) 

## Sources
 1. [Visual Guide to Quantization](https://www.maartengrootendorst.com/blog/quantization/)
 2. [Quantization of LLMs with llama.cpp](https://medium.com/@ingridwickstevens/quantization-of-llms-with-llama-cpp-9bbf59deda35)
