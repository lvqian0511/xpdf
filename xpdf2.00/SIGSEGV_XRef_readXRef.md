## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF)
files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
Xpdf 2.00 has a heap-buffer-overflow  in the function XRef::readXRef(unsigned int*) located at XRef.cc:284.
## Vulnerability details
```
ASAN:SIGSEGV
=================================================================
==91016==ERROR: AddressSanitizer: SEGV on unknown address 0x61f0bf3cce80 (pc 0x0000004aecb5 bp 0x7fff8f5e5400 sp 0x7fff8f5e5280 T0)
    #0 0x4aecb4 in XRef::readXRef(unsigned int*) /afltest/pdffonts/xpdf/XRef.cc:284
    #1 0x4afa38 in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:84
    #2 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:120
    #3 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:96
    #4 0x4b0d1e in main /afltest/pdffonts/xpdf/pdffonts.cc:117
    #5 0x7f8afd63482f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #6 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /afltest/pdffonts/xpdf/XRef.cc:284 XRef::readXRef(unsigned int*)
==91016==ABORTING
```