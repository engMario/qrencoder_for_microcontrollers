# Intro:

This library uses the qrduino code, found at https://github.com/tz1/qrduino
The qrduino is quite RAM intensive, which is makes it difficult to run on small microcontrollers.
But it does provide a tool that can reduce RAM usage. However, many users do not understand how to make use of it.
I have now got the tool and compiled it into an application that can easily be used form the host machine to generate necessary to generate the 
reduced necessary c file.
The code provided here is a reduced and modified version of the qrduino library. It only has the necessary files to generate a QR code from an input string.

# Usage:

Assuming that the generated QR code will be displayed on some sort of small screen (TFT, OLED), the size of the QR code will depend on the resolution of the screen. 
The resolution of the screen is usually given in width X length in pixels (for instance 240X400 pixels).
But the size of the QR code is expressed in modules X modules (modules are square blocks). 
A module can have more than one screen pixel, depending on how big one wants his module to be.
A module size of 0.4mm is apparently recommended for better scanning.
Once the number of pixel per module is decided, one can then calculate the maximum number of modules for a given display screen.
And based on the information found at http://www.thonky.com/qr-code-tutorial/, a QR code Version and Error Correction Level can be decided.
With the code version and error correction level at hand, now run the 'qrtool.exe' application from your command line:
Note: I have compiled this qrtool.exe on a Windows 10 machine using the 'TDM-GCC 4.9.2' 64-bit compiler from within DevC++ IDE, and I have only tested running it on a window machine also.
So open your Windows prompt, navigate to the folder with the tool and run: qrtool.exe V L V is the version (from 1-40) and L is the error correction level (from 1-4)
The qrtool.exe application will generate some code, copy that code into a c file and name it whatever you want (generated.c).
Now copy the files qr.c, qr.h and the generated c file into your application's directory. Include qr.h in your application's main file.
To use it, copy the string you want to encode to the "strinbuf" object and call qrencode(); like this:
1. strcpy((char *)strinbuf, "Your string here");
2. qrencode();
The "strinbuf" will be encoded to QR and saved to "qrframe" array.
Then we can run through the QRBIT(x,y) to get the pixels and send it to the display.
	
N.B: THIS IS A WORK IN PROGRESS, IT STILL NEED TO BE TESTED!!!	
