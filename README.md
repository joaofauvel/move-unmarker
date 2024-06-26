# Move Unmarker
Very small CLI utility to remove PII watermarks from pdfs downloaded from Move USP/ESALQ, using [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/).  
  

Beware that there is no input sanitization or error checking, you are on your own. This tool will **run**, as opposed to **work**, without fail on any 
pdf that has at least one content stream per page, which is basically every pdf in the wild. Unless the pdf has a watermark corresponding to the 2nd 
content stream of every page this will either do nothing (with the exception of removing (xml) metadata, changing compression options and maybe other 
idiosyncrasies of PyMuPDF when it comes to writing a pdf) or, in case it does have a 2 or more content streams on a page, it will keep just the first 
and likely make the file useless, though it will still open. Most pdf writers concatenate multiple content streams into one, so chances are it won't 
do anything or just crash.  
This tool will **overwrite without confirmation** any file with the same name as `--output` (default "unmarked.pdf").

## Installation
1. Make sure Python 3.8 or higher and pip are installed
1. Run `pip install move-unmarker`

## Usage
    usage: unmarker [-h] [-o OUTPUT] [-g GARBAGE] input

    Utility to remove PII watermarks from pdfs downloaded from Move USP/ESALQ.

    positional arguments:
    input                   input filename

    options:
    -h, --help              show this help message and exit
    -o OUTPUT, --output OUTPUT
                            output filename (default: "unmarked.pdf")
    -g GARBAGE, --garbage GARBAGE
                            level of garbage collection (default: 1)  
[pymupdf.Document.save](https://pymupdf.readthedocs.io/en/latest/document.html#Document.save) method for more details on garbage collection.  

### TLDR
- `unmarker watermarked.pdf`  
- `unmarker -o unmarked.pdf watermarked.pdf`  
- `unmarker --garbage 3 watermarked.pdf`

## Development
1. Check Python's version `python -V`
1. Install Python 3.8 or higher and pip, if they aren't already installed:

    - Windows `winget install Python.Python.3.X` (replace X with the desired minor version)
    - Ubuntu/Debian based distros `apt install python3 python3-pip`
    - Arch based distros `pacman -S python python-pip`
    - Fedora `dnf install python3 python3-pip`

1. [Install poetry](https://python-poetry.org/docs/#installation) 
1. Clone this repo   
`git clone https://github.com/joaofauvel/move-unmarker.git && cd move-unmarker`
1. Install requirements   
`poetry install`