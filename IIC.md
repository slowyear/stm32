# IIC注意点

1. 传输数据或者命令都是在SCL周期中完成，有high就必有low
2. 命令一般在SCL为high传输，数据（包括ack）在SCL为low传输
3. start命令： when SCL high , SDA high-down  
4. stop命令 ： when SCL high , SDA down-high
5. ack :


