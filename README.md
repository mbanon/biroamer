# biroamer

![License](https://img.shields.io/badge/License-GPLv3-blue.svg)

Biroamer is a small utility that will help you to ROAM (Random Omit Anonymize and Mix) your parallel corpus.
It will read the input TMX and output another TMX.
The resulting TMX will have its sentences randomly shuffled and omitted, mixed with another corpus, and its named entities highlighted with `<hi></hi>` tags.

## Installation instructions

### Download

```
$ git clone --recursive http://gitlab.prompsit.com/paracrawl/biroamer.git
```

### Requirements

 * Python >= 3.7
 * GNU Parallel

### Build fast_align
Install packages required by fast_align:
```
sudo apt-get install libgoogle-perftools-dev libsparsehash-dev
```

And build it:
```
$ cd fast_align
$ mkdir build
$ cd build
$ cmake ..
$ make -j
```

### Install Python requirements

```
$ pip install -r requirements.txt
$ python -m spacy download en_core_web_sm
```


## Usage

The script receives a TMX file as an input and outputs another TMX. The needed parameters are `lang1`, `lang2` and a corpus in Moses format for mixing.
```
$ cat l1-l2-file.tmx | ./biroamer.sh l1 l2 mix-corpus-l1-l2.txt > result-l1-l2.tmx
```
If your mixing corpus is in TMX format you can use `tmxt`, included in this repository, to obtain a sample in moses format:
```
cat mix-corpus.tmx | python tmxt/tmxt.py --codelist l1,l2 | head -$SIZE > mix-corpus.txt
```

## Configuration

Some of the parameters can be configured by changing variables in the `biroamer.sh` script:
 * $TOKL1 and $TOKL2: for the tokenizer scripts.
 * $PROCS: number of jobs to use in parallel, defaults to number of processes. Note that fastalign will use all the available processos regardless of the $PROCS value.
 * $BLOCKSIZE: the size of the blocks (in lines) for each parallel job. Not recommended lower than 10,000.


___

![Connecting Europe Facility](https://www.paracrawl.eu/images/logo_en_cef273x39.png)

All documents and software contained in this repository reflect only the authors' view. The Innovation and Networks Executive Agency of the European Union is not responsible for any use that may be made of the information it contains.
