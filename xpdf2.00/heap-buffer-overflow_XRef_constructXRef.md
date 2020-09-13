## What is Xpdf？
Xpdf is an open source viewer for Portable Document Format (PDF)
files.
## Version
xpdf-2.00
## Discoverers
Qian Lv and Rihan Da
## Description
In Xpdf 2.00 there is a heap buffer access overflow in XRef::constructXRef() in XRef.cc. NOTE: 2.00 is a version from November 2002.
## Vulnerability details
```
==98387==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x61f00000ee7c at pc 0x0000004b2775 bp 0x7ffd54d07330 sp 0x7ffd54d07320
READ of size 4 at 0x61f00000ee7c thread T0
    #0 0x4b2774 in XRef::constructXRef() /afltest/pdftotext/xpdf/XRef.cc:421
    #1 0x4b5f7a in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdftotext/xpdf/XRef.cc:72
    #2 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdftotext/xpdf/PDFDoc.cc:120
    #3 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdftotext/xpdf/PDFDoc.cc:96
    #4 0x4b6ed3 in main /afltest/pdftotext/xpdf/pdftotext.cc:142
    #5 0x7f6c9d87982f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)
    #6 0x4029c8 in _start (/afltest/pdftotext/xpdf/pdftotext+0x4029c8)

0x61f00000ee7c is located 4 bytes to the left of 3072-byte region [0x61f00000ee80,0x61f00000fa80)
allocated by thread T0 here:
    #0 0x7f6c9e760602 in malloc (/usr/lib/x86_64-linux-gnu/libasan.so.2+0x98602)
    #1 0x4bcd08 in grealloc /afltest/pdftotext/goo/gmem.c:129
    #2 0x4b264a in XRef::constructXRef() /afltest/pdftotext/xpdf/XRef.cc:414
    #3 0x4b5f7a in XRef::XRef(BaseStream*, GString*, GString*) /afltest/pdftotext/xpdf/XRef.cc:72
    #4 0x48ecaa in PDFDoc::setup(GString*, GString*) /afltest/pdftotext/xpdf/PDFDoc.cc:120
    #5 0x48f39c in PDFDoc::PDFDoc(GString*, GString*, GString*) /afltest/pdftotext/xpdf/PDFDoc.cc:96
    #6 0x4b6ed3 in main /afltest/pdftotext/xpdf/pdftotext.cc:142
    #7 0x7f6c9d87982f in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x2082f)

SUMMARY: AddressSanitizer: heap-buffer-overflow /afltest/pdftotext/xpdf/XRef.cc:421 XRef::constructXRef()
```