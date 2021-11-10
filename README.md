# goqr
[![GoDoc](https://godoc.org/github.com/jdomzhang/goqr?status.svg)](https://godoc.org/github.com/jdomzhang/goqr)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](/LICENSE)
[![Example](https://img.shields.io/badge/learn-example-brightgreen.svg)](/example)


This is a QR Code recognition and decoding library in pure go. It can recognize most of images into QR Code string.

# Example 

```
package main

import (
	"bytes"
	"fmt"
	"github.com/jdomzhang/goqr"
	"image"
	_ "image/jpeg"
	_ "image/png"
	"io/ioutil"
)

func recognizeFile(path string) {
	fmt.Printf("recognize file: %v\n", path)
	imgdata, err := ioutil.ReadFile(path)
	if err != nil {
		fmt.Printf("%v\n", err)
		return
	}

	img, _, err := image.Decode(bytes.NewReader(imgdata))
	if err != nil {
		fmt.Printf("image.Decode error: %v\n", err)
		return
	}
	qrCodes, err := goqr.Recognize(img)
	if err != nil {
		fmt.Printf("Recognize failed: %v\n", err)
		return
	}
	for _, qrCode := range qrCodes {
		fmt.Printf("qrCode text: %s\n", qrCode.Payload)
	}
}

func main() {
	recognizeFile("testdata/008.png")
}

```
