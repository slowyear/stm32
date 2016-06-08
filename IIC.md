# IIC注意点

1. 传输数据或者命令都是在SCL周期中完成，有high就必有low
2. 命令一般在SCL为high传输，数据（包括ack）在SCL为low传输
3. start命令： when SCL high , SDA high-down  
4. stop命令 ： when SCL high , SDA down-high
5. waitack : 在获取应答前，首先要设置SDA high  SCL high. 试想，SCL low ，这是数据传输，会发送一个数据的.
6. ack : when SCL low , SDA low . 当接受方接收完一个字节时，使SDA low,让发送发送方知道接收方已经成功接收到数据  
    code 
``IIC_SCL_CLR;    SDA_OUT();  IIC_SDA_CLR;    Delay_us(2);    IIC_SCL_SET;    Delay_us(2);   ``
7. nack : when SCL low ,SDA high 
8. sendbyte : 在SCL low时，传输数据；SCL high，数据保持不变
9. readbyte : 在SCL low时，接收数据 
10. 写数据就是写数据是新的下降沿跟新数据，上升沿锁存/读取数据，并且高位在前
读数据可以看做重复读取8次应答位，SCL的下降沿使从机跟新数据，然后主机在SCL的上升沿读取数据，此外，从机也会由高到低更新数据位
11. 空闲状态就是I2C总线总线的SDA和SCL两条信号线同时处于高电平时，规定为总线的空闲状态
