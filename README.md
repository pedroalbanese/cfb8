# CFB8
[![GoDoc](https://godoc.org/github.com/pedroalbanese/cfb8?status.png)](http://godoc.org/github.com/pedroalbanese/cfb8)
[![Go Report Card](https://goreportcard.com/badge/github.com/pedroalbanese/cfb8)](https://goreportcard.com/report/github.com/pedroalbanese/cfb8)
[![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/pedroalbanese/cfb8)](https://golang.org)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/pedroalbanese/cfb8)](https://github.com/pedroalbanese/cfb8/releases)
### Cipher Feedback Mode 8-bit of Operation for Block Ciphers
The Cipher Feedback (CFB) mode, a close relative of CBC, makes a block cipher into a self-synchronizing stream cipher. Operation is very similar; in particular, CFB decryption is almost identical to CBC encryption performed in reverse. By definition of self-synchronising cipher, if part of the ciphertext is lost (e.g. due to transmission errors), then the receiver will lose only some part of the original message (garbled content), and should be able to continue to correctly decrypt the rest of the blocks after processing some amount of input data. This simplest way of using CFB described above is not self-synchronizing. Only if a whole block size of ciphertext is lost CFB will synchronize, but losing only a single byte or bit will permanently throw off decryption. To be able to synchronize after the loss of only a single byte or bit, a single byte or bit must be encrypted at a time. CFB can be used this way when combined with a shift register as the input for the block cipher. To use CFB to make a self-synchronizing stream cipher that will synchronize for any multiple of x bits lost, start by initializing a shift register the size of the block size with the initialization vector. This is encrypted with the block cipher, and the highest x bits of the result are XOR'ed with x bits of the plaintext to produce x bits of ciphertext. These x bits of output are shifted into the shift register, and the process (starting with encrypting the shift register with the block cipher) repeats for the next x bits of plaintext. Decryption is similar, start with the initialization vector, encrypt, and XOR the high bits of the result with x bits of the ciphertext to produce x bits of plaintext, then shift the x bits of the ciphertext into the shift register and encrypt again. This way of proceeding is known as CFB-8 or CFB-1 (according to the size of the shifting). CFB shares two advantages over CBC mode with the stream cipher modes OFB and CTR: the block cipher is only ever used in the encrypting direction, and the message does not need to be padded to a multiple of the cipher block size (though ciphertext stealing can also be used to make padding unnecessary).
