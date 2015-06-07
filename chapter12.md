# HDF5

Focus on fast(partial) I/O

```
import h5py
f = h5py.File("file", "w")
f['path'] = np.array(...)
```

Chunk

* CHunks help jumping over the HDF5 file faster
* A chunk can only be loaded fully (and cached)
* Chunk too large or samll don't help, creating large index overhead

Compression and filter

* For cross-platform compatibility, use GZIP though slower
* Filter further increase the efficiency of compression

Tricky things - Strings
* Fixed-lenght ASCII/Unicode strings are supported
* Variable length? Converted to Numpy object
* Variable-length Unicode? Tricky and not cross-platform

HDF5 by default no thread safe

Pickle vs HDF5
* Pickle is no-brainer so good for prototype
* Workable for one's own class and object
* Not that workable for others Py object if not knowing the detail
* Slower than HDF5
