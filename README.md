# Hungarian (and a little bit English) raw text tokenisation 

License: GNU LGPL

2003-2004 (c) Németh László

2013-     (c) Zséder Attila

## Compile

~~~~
make
make install
~~~~

Need
- Unix environment (shell, Unix tools),
- Flex lexical analyzer generator,
- M4 macro processor.

## Usage

Need
- Unix shell, or CYGWIN on Windows
- sed

~~~~
huntoken <input_raw_text >xml_output
~~~~

## Options

- -h, --help: help
- -r: only sentence boundary detection
- -x: processing without hun_abbrev filter
- -b: break long sentences (need for tokenising long (\>4000 characters) sentences!!!)
- -n: output without XML header and footer
- -e: tokenize English (set English abbrevations)
- -v, --version: version


## Filters

See flex sources, and huntoken shell program.

László Németh
nemeth@gyorsposta.hu

Attila Zséder
zseder.hlt@gmail.com, zseder@nytud.mta.hu
