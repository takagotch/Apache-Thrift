### apache-thrift
---
https://github.com/apache/thrift

https://thrift.apache.org/

```cs
using System.IO;
using System.Threading;
using System.Threading.Tasks;

namespace Thrift.Transports.Client
{
  public class TMemoryBufferClientTransport : TClientTransport
  {
    private readonly MemoryStream _byteStream;
    private bool _isDisposed;
    
    public TMemoryBufferClientTransport()
    {
      _byteStream = new MemoryStream();
    }
    
    public TMemoryBufferClientTransport(byte[] buf)
    {
      _byteStream = new MemoryStream(buf);
    }
    
    public override bool IsOpen => true;
    
    public override async Task OpenAsync(CancellationToken cancellationToken)
    {
      if (cancellationToken.IsCancellationRequested)
      {
        await Task.FromCanceled(cancellationToken);
      }
    }
    
    public override void Close()
    {
    }
    
    
    public override async Task<int> ReadAsync(byte[] buffer, int offset, int length,
        CancellationToken cancellationToken)
    {
      return await _byteStream.ReadAsync(buffer, offset, length, cancellationToken);
    }
    
    public override async Task WriteAsync(byte[] buffer, CancellationToken cancellationToken)
    {
      await _byteStream.WriteAsyc(buffer, 0, buffer.Length, cancellationToken);
    }
    
    public override async Task WriteAsync(byte[] buffer, int offset, int length, CancellationToken cancellationToken)
    {
      await _byteStream.WriteAsync(buffer, offset, length, cancellationToken);
    }
    
    public override async Task FlushAsync(CancellationToken cancellationToken)
    {
      if (cancellationToken.IsCancellationRequested)
      {
        await Task.FromCanceled(cancellationToken);
      }
    }
    
    public byte[] GetBuffer()
    {
      return _byteStream.ToArray();
    }
    
    protected override void Dispose(bool disposing)
    {
      if (!_isDisposed)
      {
        if (disposing)
        {
          _byteStream?.Dispose();
        }
      }
      _isDisposed = true;
    }
  }
}


```

```sh
./bootstrap.sh
./configure
./configure --with-boost=/usr/local
./configure CXXFLAG='-g -02'
./configure CFLAGS='-g -02'
./configure CPPFLAGS='-DDEBBUG_MY_FEATURE'
./configure --enalbe-coverage
make 
make install
make -k check
make cross
```

```
```


