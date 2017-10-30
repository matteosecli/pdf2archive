# PDF2ARCHIVE
A simple Ghostscript-based PDF to PDF/A-1B converter.

## Requirements
+ A Bash-compatible shell
+ A recent version of Ghostscript (I tested from 9.18 to 9.22)
+ [Only if you want to validate] Java

## Installation
Just download a zip archive of this repo and unzip somewhere. If necessary, open up a terminal in the folder that you've extracted and run a `chmod +x pdf2archive`. You're done.

## Usage
Take the PDF file you want to convert and put it in the folder where you've extracted the script. Open up a terminal in the same folder and run
```
  ./pdf2archive [options] input.pdf [output.pdf]
```
where `input.pdf` is the file you want ot convert. You may or may not specify an output file name; if you don't, the output file will be automatically called `input-PDFA.pdf`. You also have a number of optional arguments:
```
  -h, --help          Show the help
  --quality=<value>   Set the quality of the output when downsampling. The possible values
                      are 'high', 'medium' and 'low', where 'high' gives the highest output
                      quality. By specifying no option, no additional downsample is done.
  --title=<value>     Title of the resulting PDF/A file
  --author=<value>    Author of the resulting PDF/A file
  --subject=<value>   Subject of the resulting PDF/A file
  --validate          Validate the resulting file. The validation is done with VeraPDF, you
                      need a working Java installation.
  --debug             Write additional debug information on screen
  -v, --version       Show the program version
```

## Examples
Convert 'input.pdf' in PDF/A-1B format; the output is 'input-PDFA.pdf':
```
  ./pdf2archive input.pdf
```

Convert 'input.pdf' in PDF/A-1B format; the output is 'output.pdf':
```
  ./pdf2archive input.pdf output.pdf
```

Convert 'input.pdf' in PDF/A-1B format and perform a high-quality compression:
```
  ./pdf2archive --quality=high input.pdf
```

Convert 'input.pdf' in PDF/A-1B format and specify the document title:
```
  ./pdf2archive --title=\"Title of your nice document\" input.pdf
```

Convert 'input.pdf' in PDF/A-1B format and validate the result:
```
  ./pdf2archive --validate input.pdf
```

## History & Motivation
This script was born as a necessity, when I had to convert the LaTeX-produced PDF of my MSc Thesis into a PDF/A-1B.

Once upon a time, the delivery of the Thesis had to be done manually, by burning a CD-ROM with the Thesis PDF on it. I don't need to say that it was extremely old-fasioned and inefficient, as you had to deliver the CD-ROM to the secretariat in person. Finally, in 2015, my university decided to activate the online submission of the PDF: you just had to upload your PDF and you were done, completely hassle-free.

Then one year ago, some _enlightened mind_ in whoever knows what administrative office, decided that a regular PDF was not easy enough; so, the university began to require the much more _satanic_ PDF/A-1B. Of course, they had to provide a set of instructions for us mere mortal, so that we could produce valid PDF/A-1B files; and indeed they did, by uploading a [_fantastic document_](http://www.biblioteca.unitn.it/282/tesi-di-laurea). If you took the (click)bait and read the PDF (not PDF/A-1B, eh!) instructions at the previous linked page, you might have noticed the _absolute completeness_ of the information contained in it: there are instructions to transform a PDF into a PDF/A-1B by either using a Windows-only free program (yeah, I know) or an obsolete OpenOffice plugin that doesn't work anymore or _paid_, commercial programs that work at most only on Windows and MacOS. No free, cross-platform alternative because hey, _everyone_ loves Windows! Naturally, you can directly produce a PDF/A-1B version of your Thesis. The document lists some easy instructions to perform a direct export into a PDF/A-1B from either Microsoft Word (or Excel, because there are people who of course write their thesis in Excel) or OpenOffice. Because _everyone_ on Earth, especially people who do Physics or Maths, write their thesis in Microsoft Word... they look _sooo beautiful_, in particular when you have to put footnotes, citations, table of contents, when Word spreads the text in a page in a zebra-style, and when you write those amazing equations in Comic Sans that get rendered as 10 DPI jpeg's. "And people who use LaTeX"? "Latex? What latex? I don't do that kind of dirty sex stuff"! - would say the guy who wrote that document. 

So you could imagine me and my friends, on the last available day for the Thesis delivery, still struggling trying to figure out how to convert. There is a [nice site](https://docupub.com/pdfconvert/) that converts PDF's into PDF/A-1B files, but there are some points:
+ your Thesis gets filled with metadata from that site, which is not nice for an official document
+ the file size limit is 10 Mb, so if you do a more experimental Thesis which is full of images you're out
+ this solution depends on someone else resources; if the site goes down tomorrow, you're in deep s***
+ it only works online, no offline alternative if you're on the move
+ you have to send personal data to an unknown site
+ you don't know what operations are being performed on your file and your data on the other side of the line

By digging around on Google, you can find people saying that you can perform the conversion via Ghostscript by just turning on a couple of switches; unfortunately, this doesn't work (the online system, Esse3, keeps saying that the file is not valid) and the matter is slightly more complicated and poorly documented. The failure in producing a valid PDF/A-1B is connected to the complex set of requirements needed, especially font embedding, metadata and color space. This script is just a collection of all the things one should to in order to obtain (in most of the cases) a valid PDF/A-1B document from a regular PDF file, in the hope that it simplifies all the process. It also contain a [free, open source validator](http://verapdf.org) that can validate the resulting file (this validator was not included in the official instructions I've linked before, which instead point to paid, commercial products).

There are still cases in which this script produces valid PDF/A-1B files which are rejected by the system because they are "too complex" and the validator used by Esse3 (our 80's-style online system programmed by [Topo Gigio](https://en.wikipedia.org/wiki/Topo_Gigio)) goes in timeout; unfortunately there is no solution that we can implement, as it's a server problem. The suspect is that they're using the commercial version of an [online validator](https://www.pdf-online.com/osa/validate.aspx) (which seems to be the only free one still working), which has the same timeout problem when validating "too complex" PDF files. This small script, instead, shows that
+ you just need a couple of lines to implement a conversion script
+ the university could just require a regular PDF file and perform the conversion with _two_ Ghostscript commands, hassle-free for the students
+ this process would be _free_, as Ghostscript is open-source
+ the inclusion of a validator is trivial, and the _free_, open source validator included here (in contrast to the validator they're using, which is _probably_ a commercial solution) can easily handle "too complex" PDF files without going in timeout

So, now the question is: what is the university still waiting for?

## FAQs

## Licensing
+ PDF2ARCHIVE is under GPLv3+
+ The included ICC file is licensed in compliance with Adobe's license agreement: https://www.adobe.com/support/downloads/iccprofiles/icc_eula_win_dist.html
+ VeraPDF is dual-licensed under MPLv2+ and GPLv3+: http://verapdf.org/home/#licensing
