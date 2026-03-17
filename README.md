# Ex2-FLASHING-OF-LEDS-WITH-LPC-1768
## AIM: 
     To interface and toggle the led with ARM LPC 1768 microprocessor           
           
## COMPONENTS REQUIRED:
 HARDWARE:
ARM LPC1768
LED
SOFTWARE:
KEIL MICRO VISION 4.0 IDE

## PROCEDURE:
⮚	Open the Keil software and select the New uvision project from Project Menu as shown below.
⮚	Browse to your project folder and provide the project name and click on save.

⮚	Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK.
⮚	Select the controller (NXP: LPC1768) and click on OK.

⮚	As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.
⮚	Create a new file by file → new to write the program.

⮚	Type the code.

⮚	After typing the code save the file as main.c eg. (abc.c).

⮚	Right click target and Add the suitable files to source group1 and header.
 
⮚	Add the main.c along with system_LPC17xx.c.

⮚	Build the project and fix the compiler errors/warnings if any.

⮚	Code is compiled with no errors. The .bin file is still not generated.
⮚	Right Click on Target Options to select the option for generating .bin file.

⮚	Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000-0x2000 so application should start from 0x2000

⮚	Write	the	command	to	generate	the .bin file	from
.axf file 
Command: fromelf --bin projectname.axf --output filename.bin
⮚	in c/c++ → include paths → desktop (00-libfiles).

⮚	.Bin file is generated after a rebuild.

⮚	Check the project folder for the generated .Bin file.


ADD FILES:
Target1:
Source group1:
Startuplpc17xx.s, delay.c , gpio.c , sysytemlpc17xx.c, main.c
Header:
delay.h, gpio.h, stdulils.h
## PROGRAM:
```
   #include <lpc17xx.h>
#include "pwm.h"
#include "delay.h"

#define CYCLE_TIME 255

/* start the main program */
int main() 
{
    int dutyCycle;
    SystemInit();             /* Clock and PLL configuration */ 
    PWM_Init(CYCLE_TIME);     /* Initialize the PWM module and the Cycle time(Ton+Toff) is set to 255(similar to arduino)*/
    PWM_Start(PWM_2|PWM_3|PWM_4|PWM_5); /* Enable PWM output on PWM_1-PWM_4 (P2_0 - P2_3) */

    while(1)
    {

        for(dutyCycle=0;dutyCycle<CYCLE_TIME;dutyCycle++) /* Increase the Brightness of the Leds */
        {
            PWM_SetDutyCycle(PWM_2,dutyCycle);  //P2_1
            PWM_SetDutyCycle(PWM_3,dutyCycle);  //P2_2
            PWM_SetDutyCycle(PWM_4,dutyCycle);  //P2_3
            PWM_SetDutyCycle(PWM_5,dutyCycle);  //P2_4
            DELAY_ms(500);
        }

        for(dutyCycle=CYCLE_TIME;dutyCycle>0;dutyCycle--) /* Decrease the Brightness of the Leds */
        {
            PWM_SetDutyCycle(PWM_1,dutyCycle);  //P2_0
            PWM_SetDutyCycle(PWM_2,dutyCycle);  //P2_1
            PWM_SetDutyCycle(PWM_3,dutyCycle);  //P2_2
            PWM_SetDutyCycle(PWM_4,dutyCycle);  //P2_3
            DELAY_ms(500);
        }
    }                              
}
```
## OUTPUT
![WhatsApp Image 2026-03-17 at 10 52 11 AM](https://github.com/user-attachments/assets/c43d312d-47f2-42f1-a3a7-682455521d26)

## RESULT:
Thus a LED is interfaced with ARM LPC1768 microprocessor and its blinking was verified successfully.
