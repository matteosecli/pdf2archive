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
