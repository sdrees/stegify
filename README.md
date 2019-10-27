# stegify
[![GoDoc](https://godoc.org/github.com/DimitarPetrov/stegify?status.svg)](https://godoc.org/github.com/DimitarPetrov/stegify)
[![Go Report Card](https://goreportcard.com/badge/github.com/DimitarPetrov/stegify)](https://goreportcard.com/report/github.com/DimitarPetrov/stegify)
[![Mentioned in Awesome Go](https://awesome.re/mentioned-badge.svg)](https://github.com/avelino/awesome-go)  


## Overview
`stegify` is a simple command line tool capable of fully transparent hiding any file within an image.
This technique is known as LSB (Least Significant Bit) [steganography](https://en.wikipedia.org/wiki/steganography) 

## Demonstration

| Carrier                                | Data                                | Result                                               |
| ---------------------------------------| ------------------------------------|------------------------------------------------------|
| ![Original File](examples/street.jpeg) | ![Encoded File](examples/lake.jpeg) | ![Encoded File](examples/test_decode.jpeg) |

The `Result` file contains the `Data` file hidden in it. And as you can see it is fully transparent.

## Install
```
$ go get -u github.com/DimitarPetrov/stegify
```

## Usage

### As a command line tool
```
$ stegify encode -carrier <file-name> -data <file-name> -result <file-name>
$ stegify decode -carrier <file-name> -result <file-name>
```
When encoding, the file with name given to flag `-data` is hidden inside the file with name given to flag
`-carrier` and the resulting file is saved in new file in the current working directory under the
name given to flag `-result`.
The result file won't have any file extension and therefore it should be specified explicitly in `-result` flag. 

When decoding, given a file name of a carrier file with previously encoded data in it, the data is extracted
and saved in new file in the current working directory under the name given to flag `-result`.
The result file won't have any file extension and therefore it should be specified explicitly in `-result` flag.

In both cases the flag `-result` could be omitted and it will be used the default file name: `result`

### Programmatically in your code

`stegify` can be used programmatically too and it provides easy to use functions working with file names
or raw Readers and Writers. You can visit [godoc](https://godoc.org/github.com/DimitarPetrov/stegify) under
`steg` package for details.

## Disclaimer

If carrier file is in jpeg or jpg format, after encoding the result file image will be png encoded (therefore it may be bigger in size)
despite of file extension specified in the result flag.