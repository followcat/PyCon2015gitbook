# Theano: A Mathematical Expression Compiler
[Get from github](https://github.com/Theano/Theano)

Goals:
* integration with NumPy
* transparent use of GPU
* efficient symbolic differentiation
* speed and stability optimizations
* dynamic C code generation

Examples:

```
import theano
a = theano.tensor.scalar('a')
b = theano.tensor.scalar('b')
c = theano.tensor.sqrt(a**2 + b**2)
sumsq = theano.function([a, b], c)
sumsq(1, 2)

array(2.23606797749979)
```
```
import theano, theano.tensor as T
X = T.matrix()
y = T.vector()
z = T.vector()
out = T.dot(X, y) * 0.6 + z *0.4
gemv = theano.function([z, X, y], out)
```
```
import theano, theano.tensor as T
x = T.scalar()
y = T.log(T.exp(x) + 1)
log1p = theano.function([x], y)
```
Performance
```
python dot.py
0.231040000916

THEANO_FLAGS=device=gpu0 python dot.py
Using gpu device 0: GeForce GTX750 Ti
0.0196080207825
```