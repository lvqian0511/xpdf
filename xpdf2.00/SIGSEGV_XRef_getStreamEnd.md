## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF)
files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
Xpdf 2.00 has a SIGSEGV  in the function XRef::getStreamEnd(unsigned int, unsigned int*) located at XRef.cc:637.
## Vulnerability details
```
ASAN:SIGSEGV
=================================================================
==89506==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000050 (pc 0x0000004ad499 bp 0x7fff8f11be80 sp 0x7fff8f11be70 T0)
    #0 0x4ad498 in XRef::getStreamEnd(unsigned int, unsigned int*) /afltest/pdffonts/xpdf/XRef.cc:637
    #1 0x48d536 in Parser::makeStream(Object*) /afltest/pdffonts/xpdf/Parser.cc:179
    #2 0x48e4aa in Parser::getObj(Object*, unsigned char*, int, int, int) /afltest/pdffonts/xpdf/Parser.cc:106
    #3 0x4abb87 in XRef::constructXRef() /afltest/pdffonts/xpdf/XRef.cc:377
    #4 0x4af8ac in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:72
    #5 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:120
    #6 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:96
    #7 0x4b0d1e in main /afltest/pdffonts/xpdf/pdffonts.cc:117
    #8 0x7f9326db082f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #9 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /afltest/pdffonts/xpdf/XRef.cc:637 XRef::getStreamEnd(unsigned int, unsigned int*)
==89506==ABORTING
```