## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF)
files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
An issue was discovered in Xpdf 2.00. There is a SIGSEGV in the function scanFont in pdffonts.cc.
## Vulnerability details
```
ASAN:SIGSEGV
=================================================================
==88615==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000010 (pc 0x0000004b01c4 bp 0x7ffdda24f640 sp 0x7ffdda24f3c0 T0)
    #0 0x4b01c3 in scanFont /afltest/pdffonts/xpdf/pdffonts.cc:222
    #1 0x4b01c3 in scanFonts /afltest/pdffonts/xpdf/pdffonts.cc:190
    #2 0x4b0fb4 in main /afltest/pdffonts/xpdf/pdffonts.cc:145
    #3 0x7f2f5a73c82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #4 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /afltest/pdffonts/xpdf/pdffonts.cc:222 scanFont
==88615==ABORTING
```