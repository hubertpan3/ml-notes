#Quantization

Quantization is the action of reducing neural network based model sizes. (Also known as "model compression")
When it comes to neural network based models each neuron often has associated weights typically represented as 32 bit floating point numbers FP32.
When training these models in the raw form tweak these weights until a particular objective is met.
This means that models using FP32 weights will require 32 bits per weight parameter.

For example, the 8 billion parameter llama3.1 8b model would require ~239 GB of space to hold all of the weights.

```
(8000000000 * 32)/1024/1024/1024 = 238.418
```

However with 4 bit quantization, we can reduce the required space down to  ~30 GB.

```
(8000000000 * 4)/1024/1024/1024 = 29.802
```

As noted in [1] 

## Sources
 1. [Visual Guide to Quantization](https://www.maartengrootendorst.com/blog/quantization/)
 2. [Quantization of LLMs with llama.cpp](https://medium.com/@ingridwickstevens/quantization-of-llms-with-llama-cpp-9bbf59deda35)
