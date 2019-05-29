## simple grpc client connection pool

```
newClient := func() (*grpc.ClientConn, error) {
    opts := []grpc.DialOption{grpc.WithInsecure(), grpc.WithBlock()}
    return grpc.Dial("your connection address", opts...)
}
pool := NewGrpcPool(newClient, 10, time.Second*30)
con, err := pool.GetConn()
if err != nil {
    panic(err)
}
if con.GetState() != connectivity.Ready {
    panic("client not ready")
}
con.Release()
```