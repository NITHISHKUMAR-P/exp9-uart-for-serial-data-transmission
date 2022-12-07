# exp9-uart-for-serial-data-transmission
### U can only run it once remember
## Code:
```
#include <LPC213x.H>              // LPC21xx definitions                      */
char a;
void uart0_init(){
  PINSEL0 = 0x00000005;           // Enable RxD0 and TxD0                     */
  U0LCR = 0x83;                   // 8 bits, no Parity, 1 Stop bit            */
  U0DLL = 97;                     // 9600 Baud Rate @ 15MHz VPB Clock         */
  U0LCR = 0x03;                   // DLAB = 0                                 */
}
void uart0_putc(char c){
 while(!(U0LSR & 0x20)); // Wait until UART0 ready to send character  
 U0THR = c; // Send character
}
int uart0_getc (void)  {                     
  while (!(U0LSR & 0x01));
  return (U0RBR);
}
int main (void)  {                
  uart0_init();      
  while (1) {                          
  a=uart0_getc();
   uart0_putc(a);
  }                               
}
```
