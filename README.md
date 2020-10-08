# STM32-Display-OLED-128x64-API

## Introduction
This API was developed as a work in the discipline of Embedded Systems Programming at UFMG - Prof. Ricardo de Oliveira Duarte - Department of Electronic Engineering

Library is developed and tested with Stm32F401RE (Nucleo 64 board) and Stm32f103c8t6 (Bluepill board). You can check the examples given.

This API is an Update to [SL-RU/stm32libs](https://github.com/SL-RU/stm32libs) API.

## Hardware and Software requirements
STM32fxxx

## Default pinout
SSD1306 | STM32Fxxx | DESCRIPTION
------------ | ------------- | -------------
VCC | 3.3V-5V | - 
GND | GND | -
SCL | PB6-PB8 |Serial clock line
SDA | PB7-PB9 |Serial data line

## API Files
	- ssd1306.c
	- ssd1306.h
	- fonts.c
	- fonts.h

__obs:__ You can access these files in oled_stm32_lib dir.

## API Configuration
	1. Download ssd1306.c, ssd1306.h, fonts.c, and fonts.h from oled_stm32_lib folder;
	2. Copy ssd1306.h and fonts.h to your Inc project folder;
	3. Copy ssd1306.c and fonts.c to your Src project folder;
	4. Select your i2c struct pointer in ssd1306.c (extern I2C_HandleTypeDef hi2c1);
	5. Include ssd1306.h where this API will be used;
	6. include your HAL project lib in ssd1306.h and fonts.h.
  
## New Features

#### void SSD1306_ShowBitmap(const unsigned char bitmap[]):
This function is responsible for displaying a 128x64 bitmap on the OLED display. In order to do so, it has a `const unsigned char[]` parameter, which is a pointer to your bitmap image.

To convert your image file to a .bmp 128x84 file you can follow the steps given by the YouTube channel [Controllers Tech](https://www.youtube.com/channel/UCkdqtSMnhYuMsJkyHOxiPZQ) in their [video](https://www.youtube.com/watch?v=M5ddTjrcvEs). 

Instead of creating different .h files for differente bitmaps, you may create a unique .h file with all the bitmaps you want.

![Show bmp feature](https://github.com/guiguitz/STM32-Display-OLED-128x64-API/blob/main/github_images/show_bmp.jpg)

#### void SSD1306_ShowGif(uint8_t n_frames, ...):
Similarly to the previous function, this function is responsible for displaying a sequence of 128x64 frames on the OLED display. By showing a sequence of 			frames in a high frequency, it gives us the impression of an animation playing on the screen.

The function has a fixed parameter `uint8_t n_frames` to informe the number of frames used. The others parameters should be pointers to bitmaps representing each frame of the entire animation.

It is also recommended following the steps given by the the YouTube channel [Controllers Tech](https://www.youtube.com/channel/UCkdqtSMnhYuMsJkyHOxiPZQ) in their [video](https://www.youtube.com/watch?v=M5ddTjrcvEs) for creating the animation .h file and converting correctly frames to 128x64 .bmp file.

__Example:__
```C
SSD1306_ShowGif(12, horsegif1, horsegif2, horsegif3, horsegif4, horsegif5, horsegif6, horsegif7, horsegif8, horsegif9, horsegif10, horsegif11, horsegif12);
SSD1306_ShowGif(12, horsegif1, horsegif2, horsegif3, horsegif4, horsegif5, horsegif6, horsegif7, horsegif8, horsegif9, horsegif10, horsegif11, horsegif12);
SSD1306_ShowGif(12, horsegif1, horsegif2, horsegif3, horsegif4, horsegif5, horsegif6, horsegif7, horsegif8, horsegif9, horsegif10, horsegif11, horsegif12);
```

#### void SSD1306_Counter(uint8_t seconds):
This is a very simple function which works as a cronometer or a counter, displaying the current second on the 128x64 OLED display. When it reaches the time limit, given 	by the function's parameter, the counter stops.

#### void SSD1306_Println(char* format, ...):
This function works as a println function for the 128x64 OLED display. 

It takes a string that contains the text to be written and, optionally, contain embedded format tags that are replaced by the values specified in subsequent additional arguments and formatted as requested. Format tags prototype is `%[flags][width][.precision][length]` specifier. Click on this link to have a complete printf reference: [Link](https://www.tutorialspoint.com/c_standard_library/c_function_printf.htm)

The user can use it as a debug system to print program variables in a easy way.

__Example:__
```C
for (uint8_t i = 0; i < 10; i++)
{
    SSD1306_Println("var1 = %i", i);
    SSD1306_Println("var2 = %d", i*3);
    SSD1306_Println("var3 = %i", i*4);
    HAL_Delay(1000);
}
```

![println feature](https://github.com/guiguitz/STM32-Display-OLED-128x64-API/blob/main/github_images/println.jpg)

## All Features
* uint8_t SSD1306_Init(void);
* void SSD1306_UpdateScreen(void);
* void SSD1306_ToggleInvert(void);
* void SSD1306_Fill(SSD1306_COLOR_t Color);
* void SSD1306_DrawPixel(uint16_t x, uint16_t y, SSD1306_COLOR_t color);
* void SSD1306_GotoXY(uint16_t x, uint16_t y);
* char SSD1306_Putc(char ch, FontDef_t* Font, SSD1306_COLOR_t color);
* char SSD1306_Puts(char* str, FontDef_t* Font, SSD1306_COLOR_t color);
* void SSD1306_DrawLine(uint16_t x0, uint16_t y0, uint16_t x1, uint16_t y1, SSD1306_COLOR_t c);
* void SSD1306_DrawRectangle(uint16_t x, uint16_t y, uint16_t w, uint16_t h, SSD1306_COLOR_t c);
* void SSD1306_DrawFilledRectangle(uint16_t x, uint16_t y, uint16_t w, uint16_t h, SSD1306_COLOR_t c);
* void SSD1306_DrawTriangle(uint16_t x1, uint16_t y1, uint16_t x2, uint16_t y2, uint16_t x3, uint16_t y3, SSD1306_COLOR_t color);
* void SSD1306_DrawCircle(int16_t x0, int16_t y0, int16_t r, SSD1306_COLOR_t c);
* void SSD1306_DrawFilledCircle(int16_t x0, int16_t y0, int16_t r, SSD1306_COLOR_t c);
* void SSD1306_ScrollRight(uint8_t start_row, uint8_t end_row);
* void SSD1306_ScrollLeft(uint8_t start_row, uint8_t end_row);
* void SSD1306_Scrolldiagright(uint8_t start_row, uint8_t end_row);
* void SSD1306_Scrolldiagleft(uint8_t start_row, uint8_t end_row);
* void SSD1306_Stopscroll(void);
* void SSD1306_InvertDisplay (int i);
* void SSD1306_Clear (void);
* void SSD1306_DrawBitmap(int16_t x, int16_t y, const unsigned char* bitmap, int16_t w, int16_t h, uint16_t color);
* void SSD1306_ShowBitmap(const unsigned char bitmap[]);
* void SSD1306_ShowGif(uint8_t n_frames, ...);
* void SSD1306_Counter(uint8_t seconds);
* void SSD1306_Println(char* format, ...);

## Contact the Authors
Guilherme Amorim: `guilherme.vini65@gmail.com`

Renan Guedes: `rbguedes1998@gmail.com`
