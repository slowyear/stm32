# IIC注意点

1. 传输数据或者命令都是在SCL周期中完成，有high就必有low
2. 命令一般在SCL为high传输，数据（包括ack）在SCL为low传输
3. start命令： when SCL high , SDA high-down  
4. stop命令 ： when SCL high , SDA down-high
5. waitack : 在获取应答前，首先要设置SDA high  SCL high. 试想，SCL low ，这是数据传输，会发送一个数据的.
6. ack : when SCL low , SDA low 
   code : '	IIC_SCL_CLR;
	          SDA_OUT();
	          IIC_SDA_CLR;
	          Delay_us(2);
	          IIC_SCL_SET;
          	Delay_us(2);'


