# ePaper-7inch5-partial-display
ePaper 7.5 MicroPython Partial Display Raspberry Pi Pico

When I started playing around with my Waveshare ePaper 7.5 V2 (monochrome), I quickly discovered that in the sample code Waveshare created, the section on partial code was commented out. Various web searches gave no clue as to how this make this work in MicroPython, so I set out to work trying to see if I could solve this puzzle. I think I did.

I added another framebuffer in the Waveshare driver, specifically for the partial display. Partial display would work after this change, but most of the time, text was garbled. I couldn't figure out why.

The big breakthrough came when, after many hours of trial and error, I discovered that for partial display to work properly, the area you have designated as partial must be placed on the screen such that the last column of your area lands on a column of the overall screen area which is either 80,160,240,320,400,480,560,640,720 or 800, in other words divisible by 80. It doesn't matter how narrow or wide or how deep your area is, the very right column needs to be on a main screen column divisble by 80. Your area may overlap an 80 column boundary, e.g. you have a column width of 110.

The other quirky thing is that the colors on the partial area appear the be reversed, i.e. if you tell it to print white, it prints black and vice versa.

The MicroPython version I am using is 1.21.0
