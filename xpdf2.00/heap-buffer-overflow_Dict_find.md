## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF)
files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
Xpdf 2.00 has a heap-buffer-overflow  in the function Dict::find(char*) located at Dict.cc:56.
## Vulnerability details
```
==90691==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60300000ca14 at pc 0x00000040df7e bp 0x7ffc91b07720 sp 0x7ffc91b07710
READ of size 4 at 0x60300000ca14 thread T0
    #0 0x40df7d in Dict::find(char*) /afltest/pdffonts/xpdf/Dict.cc:56
    #1 0x40df7d in Dict::lookup(char*, Object*) /afltest/pdffonts/xpdf/Dict.cc:72
    #2 0x4ac635 in Object::dictLookup(char*, Object*) /afltest/pdffonts/xpdf/Object.h:252
    #3 0x4ac635 in XRef::checkEncrypted(GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:459
    #4 0x4afbcd in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:107
    #5 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:120
    #6 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:96
    #7 0x4b0d1e in main /afltest/pdffonts/xpdf/pdffonts.cc:117
    #8 0x7fbd2fd8f82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #9 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

0x60300000ca16 is located 0 bytes to the right of 22-byte region [0x60300000ca00,0x60300000ca16)
allocated by thread T0 here:
    #0 0x7fbd30c76602 in malloc (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x98602)
    #1 0x4b6788 in gmalloc /afltest/pdffonts/goo/gmem.c:89
    #2 0x4b6885 in copyString /afltest/pdffonts/goo/gmem.c:201
    #3 0x48690f in Object::copy(Object*) /afltest/pdffonts/xpdf/Object.cc:86
    #4 0x48e3a8 in Parser::getObj(Object*, unsigned char*, int, int, int) /afltest/pdffonts/xpdf/Parser.cc:151
    #5 0x4abb87 in XRef::constructXRef() /afltest/pdffonts/xpdf/XRef.cc:377
    #6 0x4af8ac in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:72
    #7 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:120
    #8 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:96
    #9 0x4b0d1e in main /afltest/pdffonts/xpdf/pdffonts.cc:117
    #10 0x7fbd2fd8f82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)

SUMMARY: AddressSanitizer: heap-buffer-overflow /afltest/pdffonts/xpdf/Dict.cc:56 Dict::find(char*)
```