# node-xdelta3

Asynchronous, non-blocking Node.js binding for Xdelta3 binary diff utility

# API

**xdelta3.DiffStream(fd src, fd dst)**  
src - original file  
dst - file to generate diff with  
creates a readable stream  

**xdelta3.PatchStream(fd src, fd dest);**  
src - original file  
dest - file generated from diff  
creates a writable stream  

# USAGE

``` js
var aDelta = new xdelta3.DiffStream(src, dst);
aDelta.on('data', function(bufferChunk) {
  console.log('chunk of diff received');
});
aDelta.on('end', function() {
  console.log('diff finished');
});
aDelta.on('error', function(err) {
  console.log('error: ' + err);
});

var aPatch = new xdelta3.PatchStream(src, dst);
for (var N = 0; N < aDiffBufferChunks.length; N++)
  aPatch.write(aDiffBufferChunks[i]);
aPatch.end();
aPatch.on('error', function(err) {
  console.log('error: ' + err);
});
aPatch.on('finish', function() {
  console.log('patch finished');
});

```

# DEPENDENCIES

This binding requires the existence of libxdelta3.a in a shared library path:

* download the sources for a stable release - [3.0.6 here ](ttps://code.google.com/p/xdelta/source/browse/trunk/xdelta3/releases/xdelta3-3.0.6.tar.gz)
* build the command line interface
* create the library from the existing objects:
```
ar cr libxdelta3.a xdelta-xdelta3.o
```
* move the library to a shared lib path (ex /usr/local/lib)

