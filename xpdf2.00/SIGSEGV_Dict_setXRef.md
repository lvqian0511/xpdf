## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF) files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
Xpdf 2.00 has a SIGSEGV in Dict::setXRef(XRef*) in Dict.h.
## Vulnerability details
```
ASAN:SIGSEGV
=================================================================
==88710==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000000 (pc 0x0000004afb78 bp 0x7fff04ba6480 sp 0x7fff04ba63b0 T0)
    #0 0x4afb77 in Dict::setXRef(XRef*) /afltest/pdffonts/xpdf/Dict.h:64
    #1 0x4afb77 in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdffonts/xpdf/XRef.cc:101
    #2 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:120
    #3 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdffonts/xpdf/PDFDoc.cc:96
    #4 0x4b0d1e in main /afltest/pdffonts/xpdf/pdffonts.cc:117
    #5 0x7f6543b3c82f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #6 0x4029c8 in _start (/afltest/pdffonts/xpdf/pdffonts+0x4029c8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /afltest/pdffonts/xpdf/Dict.h:64 Dict::setXRef(XRef*)
==88710==ABORTING
```