---
title: "PicoCTF Challenge: Information (#186)"
seoDescription: "Workaround and solution of PicoCTF Challenge: Information (#186)."
datePublished: Tue Jun 22 2021 10:53:59 GMT+0000 (Coordinated Universal Time)
cuid: ckq7xjuo1006k8qs1eyg8ej2l
slug: picoctf-challenge-information-186
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1624356490694/3K5a570nc.jpeg
tags: security, images

---

## Overview

- Point: 10
- Category: Forensics
- Author: SUSIE
- Link:  [https://play.picoctf.org/practice/challenge/186](https://play.picoctf.org/practice/challenge/186) 

## Description

Files can always be changed in a secret way. Can you find the flag? cat.jpg.

## Hints

- Look at the details of the file.
- Make sure to submit the flag as picoCTF{XXXXX}.

## Workaround

By the details above, we can understand that the flag is hidden somewhere inside the image. My first approach was looking at the cute cat in the image. LOL 😅.


### Approach 1
At first, I have tried to use the `strings` and `grep` command to retrieve the flag. 

```txt
hsblhsn-picoctf@webshell:~$ strings cat.jpg | grep pico
hsblhsn-picoctf@webshell:~$ strings cat.jpg | grep CTF 
PicoCTF
    <rdf:li xml:lang='x-default'>PicoCTF</rdf:li>
hsblhsn-picoctf@webshell:~$ strings cat.jpg | grep flag
hsblhsn-picoctf@webshell:~$
```
But no luck. We have found no useful information or almost no information.

### Approach 2

Then I have tried to get the image information by the `identify` command provided by the `imagemagick` tool. But found almost no useful information.

```txt
hsblhsn-picoctf@webshell:~$ identify -verbose cat.jpg
Image: cat.jpg
  Format: JPEG (Joint Photographic Experts Group JFIF format)
  Mime type: image/jpeg
  Class: DirectClass
  Geometry: 2560x1598+0+0
  Units: Undefined
  Colorspace: sRGB
  Type: TrueColor
  Base type: Undefined
  Endianess: Undefined
  Depth: 8-bit
  Channel depth:
    red: 8-bit
    green: 8-bit
    blue: 8-bit
  Channel statistics:
    Pixels: 4090880
    Red:
      min: 0  (0)
      max: 255 (1)
      mean: 77.7595 (0.304939)
      standard deviation: 66.715 (0.261627)
      kurtosis: -0.957235
      skewness: 0.462007
      entropy: 0.898738
    Green:
      min: 0  (0)
      max: 255 (1)
      mean: 73.0898 (0.286626)
      standard deviation: 73.7297 (0.289136)
      kurtosis: -0.661389
      skewness: 0.725565
      entropy: 0.875171
    Blue:
      min: 0  (0)
      max: 255 (1)
      mean: 78.7632 (0.308875)
      standard deviation: 73.1169 (0.286733)
      kurtosis: -0.388597
      skewness: 0.811307
      entropy: 0.913713
  Image statistics:
    Overall:
      min: 0  (0)
      max: 255 (1)
      mean: 76.5375 (0.300147)
      standard deviation: 71.1872 (0.279166)
      kurtosis: -0.62324
      skewness: 0.681315
      entropy: 0.895874
  Rendering intent: Perceptual
  Gamma: 0.454545
  Chromaticity:
    red primary: (0.64,0.33)
    green primary: (0.3,0.6)
    blue primary: (0.15,0.06)
    white point: (0.3127,0.329)
  Background color: white
  Border color: srgb(223,223,223)
  Matte color: grey74
  Transparent color: black
  Interlace: None
  Intensity: Undefined
  Compose: Over
  Page geometry: 2560x1598+0+0
  Dispose: Undefined
  Iterations: 0
  Compression: JPEG
  Quality: 90
  Orientation: Undefined
  Properties:
    date:create: 2021-06-22T09:54:25+00:00
    date:modify: 2021-03-15T18:24:46+00:00
    jpeg:colorspace: 2
    jpeg:sampling-factor: 2x2,1x1,1x1
    signature: d69bb6806fb38483ab0f5d5c1e725c8752c12803059cd25895f0e600b8e4f33a
  Profiles:
    Profile-8bim: 32 bytes
    Profile-iptc: 19 bytes
      Copyright String[2,116]: PicoCTF
      unknown[2,0]: 
    Profile-xmp: 3034 bytes
  Artifacts:
    filename: cat.jpg
    verbose: true
  Tainted: False
  Filesize: 878136B
  Number pixels: 4090880
  Pixels per second: 21.5309MB
  User time: 0.050u
  Elapsed time: 0:01.190
  Version: ImageMagick 6.9.10-23 Q16 x86_64 20190101 https://imagemagick.org
```

### Approach 3
After the failed attempts, I have tried the `exiftool` command. And found a little bit useful information. 

```txt
hsblhsn-picoctf@webshell:~$ exiftool cat.jpg
ExifTool Version Number         : 11.88
File Name                       : cat.jpg
Directory                       : .
File Size                       : 858 kB
File Modification Date/Time     : 2021:03:15 18:24:46+00:00
File Access Date/Time           : 2021:06:22 09:56:53+00:00
File Inode Change Date/Time     : 2021:06:22 09:54:25+00:00
File Permissions                : rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```
Did you see anything suspicious in the `License` field of the output? It's a valid base 64 string. So let's decode it and see what's inside.

```txt
hsblhsn-picoctf@webshell:~$ echo 'cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9' | base64 -d
picoCTF{the_m3tadata_1s_modified}
```
Yay! We got the flag!

### Flag

```txt
 picoCTF{the_m3tadata_1s_modified}
```

Thank you for reading! Here is a potato.



![Here is a potato](https://cdn.hashnode.com/res/hashnode/image/upload/v1624371543959/E-GIOA1xJ.jpeg)
<sup><sub>
 Photo by <a href="https://unsplash.com/@lukasz_rawa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Łukasz Rawa</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>.
</sup></sub>




