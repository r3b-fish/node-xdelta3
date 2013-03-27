# node-xdelta3

Asynchronous, non-blocking Node.js binding for Xdelta3 binary diff utility

# API

**xdelta3.diff(fd src, fd dst)**  
src - original file  
dst - file to generate diff with  
returns a readable stream  

**xdelta3.patch(fd src, fd dest, callback);**  
src - original file  
dest - file generated from diff  
callback - it is called with err as a parameter once the output has been generated  
return a writable stream  

# USAGE


``` js
var aDelta = xdelta3.diff(src, dst);
aDelta.on('data', function(bufferChunk) {
  console.log('chunk of diff received');
});
aDelta.on('end', function() {
  console.log('diff finished');
});
aDelta.on('error', function(err) {
  console.log('error: ' + err);
});

var aPatch = xdelta3.patch(src, dst, function(err){ console.log('done'); });
for (var N = 0; N < aDiffBufferChunks.length; N++)
  aPatch.write(aDiffBufferChunks[i]);
aPatch.end();
```
