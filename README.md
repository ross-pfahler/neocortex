# neuralnet-predict.js

Run trained neural networks in the browser or node.js.

### Background

Training deep neural networks on any meaningful dataset requires massive computational resources and lots and lots of time. However, prediction is relatively cheap - there is no backpropagation, computational graphs, loss functions, or optimization algorithms to worry about or that needs to be implemented (online learning is a different story). What do you do when you want your neural network to power a part of your client-facing web application? Traditionally, you would deploy your model on a server and call it from your web application through an API. What if you can deploy it _in the browser_ alongside the rest of your webapp? Computation would be offloaded entirely to your end-user!

A pipe dream? Perhaps most users will not be able to run billion-parameter networks in their browsers quite yet, but smaller networks are certainly within the realm of possibility!

By focusing purely on prediction of already trained neural networks, we can take into full consideration the constraints of client hardware and the capabilities of current browsers. Given a neural network architecture and pre-trained weights, we can focus on making forward predictive passes through the network as computationally efficient as possible.

Computation on GPU is perfomed where possible and advantageous to do so. This is currently implemented using WebGL (hopefully WebCL will in the future make things more interesting).

What about using emscripten to compile models to asm.js? It may be within the realm of possibility (especially with the coming of WebAssembly), but this would be quite heavy and not so trivial (see Cyrille Rosant's [attempts](http://cyrille.rossant.net/numpy-browser-llvm/) at running numpy in the browser through Numba and LLVM). By only focusing only on the prediction phase, we can be as light and minimal as possible. The ultimate goal of this project is to be able to serialize a Keras or Caffe model together with pretrained weights into javascript, pack it in your webapp, and be off and running.

I'd be remiss if I didn't credit Andrej Karpathy's [ConvNetJS](https://github.com/karpathy/convnetjs) as a source of inspiration, as well as the excellent Theano-based deep learning framework [Keras](https://github.com/fchollet/keras/). 

### Usage


### API

Functions and layers currently implemented are listed below. More forthcoming.

##### Activation functions

+ `linear`

+ `relu` (rectified linear or ReLU)

+ `sigmoid` or `sigmoidHard`

+ `tanh`

+ `softmax`

##### Dense fully-connected layers

+ `denseLayer`

##### Recurrent layers

+ `rGRULayer` (gated-recurrent unit or GRU)

+ `rLSTMLayer` (long short-term memory or LSTM)

+ `rJZS1Layer`, `rJZS2Layer`, `rJZS3Layer` (mutated GRUs - JZS1, JZS2, JZS3 - from [Jozefowicz et al. 2015](http://jmlr.org/proceedings/papers/v37/jozefowicz15.pdf))

##### Convolutional layers

+ `convolution1DLayer`

+ `convolution2DLayer`

+ `pooling1DLayer`

+ `pooling2DLayer`

##### Embedding layers

+ `embeddingLayer` - maps indices to corresponding embedding vectors

##### Normalization layers

+ `batchNormalizationLayer` - see [Ioffe and Szegedy 2015](http://arxiv.org/abs/1502.03167)

### Build

```
$ npm run build
```

##### Webpack



### Tests

```
$ npm test
```

Note: tests for SIMD code uses a [shim/polyfill](https://github.com/ljharb/simd) based on the [ES7 proposal](https://github.com/tc39/ecmascript_simd). The only browser that currently support SIMD is firefox nightly build.

Browser testing is planned.

### Colophon

&copy; 2015 Leon Chen. MIT License.
