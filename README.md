# stm32  注意点

## printf重载  
1.在头文件中包含"stdio.h"

/* Includes ------------------------------------------------------------------*/
/#include "main.h"

/#include "stdio.h"

2.宏定义       

/* Private function prototypes -----------------------------------------------*/
/#ifdef __GNUC__
  /* With GCC/RAISONANCE, small printf (option LD Linker->Libraries->Small printf
     set to 'Yes') calls __io_putchar() */
  #define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
/#else
  #define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)
/#endif /* __GNUC__ */

如果在这段程序之前__GNUC__ 被定义过，就执行 #define PUTCHAR_PROTOTYPE int __io_putchar(int ch)，即将PUTCHAR_PROTOTYPE宏定义为int __io_putchar(int ch)，则在以后的程序中见到PUTCHAR_PROTOTYPE便用int __io_putchar(int ch)来替代；

如果__GNUC__ 在之前没有被定义过，则执行#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)；

3.定义PUTCHAR_PROTOTYPE


/**
  * @brief  Retargets the C library printf function to the USART.
  * @param  None
  * @retval None
  */
PUTCHAR_PROTOTYPE
{
  /* Place your implementation of fputc here 执行*/
  /* e.g. write a character to the EVAL_COM1 and Loop until the end of transmission */
  HAL_UART_Transmit(&UartHandle, (uint8_t *)&ch, 1, 0xFFFF);

  return ch;
}

这里是实现printf功能的，其中UartHandle可以修改为你所设置的串口号，当然HAL_UART_Transmit也是可以修改的。

4.在主函数中使用printf

  /* Output a message on Hyperterminal 超级终端 using printf function */
  printf("\n\r UART Printf Example: retarget the C library printf function to the UART\n\r");


  ## nather
