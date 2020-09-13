## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF) files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
Xpdf 2.00 has a heap-buffer-overflow  in the function Object::fetch(XRef*, Object*) located at Object.cc:98.
## Vulnerability details
```
==90184==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x61a00001f780 at pc 0x00000048695e bp 0x7ffeefb9e5a0 sp 0x7ffeefb9e590
READ of size 4 at 0x61a00001f780 thread T0
    #0 0x48695d in Object::fetch(XRef*, Object*) /afltest/pdffonts/xpdf/Object.cc:98
    #1 0x403e56 in Array::get(int, Object*) /afltest/pdffonts/xpdf/Array.cc:49
    #2 0x44a525 in Object::arrayGet(int, Object*) /afltest/pdffonts/xpdf/Object.h:228
    #3 0x44a525 in Gfx8BitFont::Gfx8BitFont(XRef*, char*, Ref, GString*, GfxFontType, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:710
    #4 0x44d5dc in GfxFont::makeFont(XRef*, char*, Ref, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:113
    #5 0x44d9c4 in GfxFontDict::GfxFontDict(XRef*, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:1262
    #6 0x4b00bc in scanFonts /afltest/pdffonts/xpdf/pdffonts.cc:187
    #7 0x4b0fb4 in main /afltest/pdffonts/xpdf/pdffonts.cc:145
    #8 0x7f584c81982f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #9 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

0x61a00001f780 is located 0 bytes to the right of 1280-byte region [0x61a00001f280,0x61a00001f780)
allocated by thread T0 here:
    #0 0x7f584d700961 in realloc (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x98961)
    #1 0x4b6806 in grealloc /afltest/pdffonts/goo/gmem.c:127
    #2 0x403d52 in Array::add(Object*) /afltest/pdffonts/xpdf/Array.cc:42
    #3 0x48dc33 in Object::arrayAdd(Object*) /afltest/pdffonts/xpdf/Object.h:225
    #4 0x48dc33 in Parser::getObj(Object*, unsigned char*, int, int, int) /afltest/pdffonts/xpdf/Parser.cc:73
    #5 0x4ad37b in XRef::fetch(int, int, Object*) /afltest/pdffonts/xpdf/XRef.cc:608
    #6 0x4869cb in Object::fetch(XRef*, Object*) /afltest/pdffonts/xpdf/Object.cc:99
    #7 0x40e025 in Dict::lookup(char*, Object*) /afltest/pdffonts/xpdf/Dict.cc:72
    #8 0x44a49b in Gfx8BitFont::Gfx8BitFont(XRef*, char*, Ref, GString*, GfxFontType, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:706
    #9 0x44d5dc in GfxFont::makeFont(XRef*, char*, Ref, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:113
    #10 0x44d9c4 in GfxFontDict::GfxFontDict(XRef*, Dict*) /afltest/pdffonts/xpdf/GfxFont.cc:1262
    #11 0x4b00bc in scanFonts /afltest/pdffonts/xpdf/pdffonts.cc:187
    #12 0x4b0fb4 in main /afltest/pdffonts/xpdf/pdffonts.cc:145
    #13 0x7f584c81982f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)

SUMMARY: AddressSanitizer: heap-buffer-overflow /afltest/pdffonts/xpdf/Object.cc:98 Object::fetch(XRef*, Object*)
```