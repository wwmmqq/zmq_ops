
## TensorFlow ZMQ Op

+ Send a list of numpy arrays from python; serialization is written in C++ for efficiency.
  + One copy in merging all the buffers; One copy in pybind11 overhead (TODO); One copy in ZMQ send.
+ Receive a list of tensors from tensorflow;
  + One copy in ZMQ recv; One copy to split the buffer into tensors.
  + The op is stateful and safe to be evaluated multiple times in one `sess.run` call.
+ Serialization is in a custom protocol for efficiency;

## Build:

Install libzmq, as well as the `zmq.hpp` header from cppzmq.

Then, `make`

## Use:

See `benchmark.py` for usage.

On my machine this script can achieve about 1.3G/s throughput (i.e. 2.3k float32 imagenet images per second).
