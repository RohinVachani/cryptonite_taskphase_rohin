# **Forensics**

## **ShunyaCTF- CorruptedPNG**

First check the file type, `file corrupted_flag.png`

```
corrupted_flag.png: PNG image data, 288 x 27, 1-bit colormap,
```
Use `pngcheck corrupted_flag.png` to identify the problem
```
corrupted_flag.png  invalid IHDR interlace method (82)
```
I have used `xxd` hexdeitor
`xxd corrupted_flag.png`
```
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 0120 0000 001b 0103 0000 5263 e2f0  ... ........Rc..
00000020: c100 0000 0173 5247 4245 aece 1ce9 0000  .....sRGBE......
00000030: 0004 6741 4d41 0000 b150 0bfc 6105 0000  ..gAMA...P..a...
00000040: 0006 504c 5445 ffff ff00 0041 55c2 d37e  ..PLTE.....AU..~
00000050: 0000 0009 7048 5973 0000 0ec3 0000 0ec3  ....pHYs........
00000060: 52c7 6fa8 6400 0001 4b49 4441 5438 cbed  R.o.d...KIDAT8..
00000070: d0b1 4ac3 5014 06e0 132e 340e 0793 d2e5  ..J.P.....4.....
00000080: 0ac5 22be c00d 0e2a 04c4 a5cf d11a 7172  .."....*......qr
00000090: c818 7168 a4a0 6ef6 014a 9f25 7243 261f  ..qh..n..J.%rC&.
000000a0: a083 c3ed 5247 f304 d673 6e12 aa52 0a0e  ....RG...sn..R..
000000b0: 6e1e 9270 72f9 38e7 4fe0 bfb8 dce9 b757  n..pr.8.O......W
000000c0: c738 a96d b2fa 2006 3705 f4b9 c5fa c8d3  .8.m.. .7.......
000000d0: c048 9416 49ba 7dc0 4c54 28ac 118a 0a55  .H..I.}.LT(....U
000000e0: 9312 8b76 0635 bade 88e6 16c9 06e1 4654  ...v.5........FT
000000f0: ad93 c3f7 d524 9997 80fb e066 a03d f4e6  .....$.....f.=..
00000100: c354 dc68 485e 7b2d 23c3 e329 a1a8 832a  .T.hH^{-#..)...*
00000110: 5f3c 0206 b41a b47c 1a4b 42b3 c8e4 cb83  _<.....|.KB.....
00000120: 0725 2f4e 9784 ae04 06a9 a635 0a80 115d  .%/N.......5...]
00000130: 8470 10a4 8573 afe4 4015 1218 9d5b 7462  .p...s..@....[tb
00000140: 5117 a20a ed55 2856 05c2 7a12 6532 94e9  Q....U(V..z.e2..
00000150: 0bea 110a 9b49 6d8b 5c40 9a24 d235 0a08  .....Im.\@.$.5..
00000160: edaa 8232 f51b 242c 727e a016 23d4 1df4  ...2..$,r~..#...
00000170: f367 faba 4340 036f ed89 ee2e 085d aabc  .g..C@.o.....]..
00000180: 3822 d467 e4de 2d5e fc24 2b61 34e3 4cb7  8".g..-^.$+a4.L.
00000190: 9e37 f678 5264 12ce b40a 1981 fda5 5beb  .7.xRd........[.
000001a0: 17a8 bb1d c54d e37e 008c 0c3f b9ce 4af8  .....M.~...?..J.
000001b0: 8b02 f804 9ec2 7649 b765 81cc 0000 0000  ......vI.e......
000001c0: 4945 4e44 ae42 6082                      IEND.B`.
```
The first four bytes are "png signature", after this we can view the IHDR chunk.
First 4 bytes tell us the size of IHDR data, which is 13. The next 4 bytes is for the chunk type, which is IHDR in hex encoding. The next 13 bytes is for the IHDR data and the following 4 bytes is the CRC32 value calculated on these 13 bytes.

The 13th byte is interlace value, and valid values are 00 or 01. So we edit this value to 00.

`xxd corrupted_flag.png > corrupted_flag.hex` to create the hex-dump and use nano to edit the value.

After editing, we revert the edited hexdump to png file.

`xxd -r corrupted_flag.hex fixed.png`

We use `pngcheck` to verify if it has been fixed, its not!
The `CRC` value of IHDR is incorrect so we have to fix that as well.

After this , the rendering value of the `sGRB` chunk( ascii string is in the third line) is set incorrectly.
```
00000020: c100 0000 0173 5247 4245 aece 1ce9 0000  .....sRGBE......
```
The byte after `0173 5247 42` has to be changed to a valid value, `00`,`01`,`02`,`03`.

When this is fixed , we have to similarly fix the CRC values in the `gAMA` and `PLTE` chunks.

The unit specifier byte and CRC value of `pHYs` has to be fixed too.



















