## Understanding cards in our wallet

I recently brought a Mi band 4 with NFC support, however xiaomi seems not willing to give consumers permission to custom their simulated cards, e.g. only cards without encryption can be simulated or they give you a so-called "Mi blank card". What is that? How do the NFC simulation works and is there any to hack it? I decide to write a review for my future reminder. I would be pleasant if this post is helping for anyone who reads. I a native Chinese speaker however I was too lazy to install Chinese IME in my Linux Mint computer, so lots of my works including this one would be delivered in my broken English. I know how to install Chinese IME, it's easy, but I am lazy.

Now you see the reason I named this repository "blah-blah". In Chinese, we call this constantly talking without proper focus as "broken mouth". Now I am writing breaking English with my "broken mouth". :)

### !!! still working on it !!! if you are finding solution on your own issue, this post is not helping, posts would be updated later in chinese.!!!

### RFID (Radio-Frequency IDentification)


Thought UID is designed to be unique on earth, we marvelous Chinese engineers found the way to clone such a protected rule and _Chinese magic cards_ born. I brought 10 UID changable cards on _taobao.com_ at a cost of less than one dollor with free shipping. 

Here is a description I found on ebay, obvious that's a similar product.
>Description
>
>UID Changeable 1K Card  RFID 13.56MHz ISO14443A Block 0 sector zero writable HF IC Copy Clone MF1 1K S50 support NFC Cracker 
>This card works the same as the normal IC cards, for MF1 1K S50 standard.      
>Only the Sector 0 Block Zero which is known as the Serial Number/Manufacturers Block(Chip UID) could be programmed to any UID you want.Usually we use NFC ACR122U (PN532) reader via Libnfc/M1fare Card Recovery Tool/MFGUI etc. Proxmark3,or many MF writer copier support
>
>Specifications
>- Frequency: 13.56 MHz
>- Protocol: ISO14443A
>- Capacity: 1k bytes EEPROM memory    
>- Rewrite Times:  100,000 times
>- Read Distance: 0 ~ 10 cm(depends on the R/W device)  
>- Material: ABS 
>
>Features
>1. User definable access conditions & password for each memory block
>2. Organized in 16 sector with 4 blocks of 16 bytes each (one block consists of 16 byte)   
>3. Perfectly work with NFC ACR122U read-writer/ Proxmark3 / Icopy 3 
>4. Each block rewritable and useful



I found [this post](https://stackoverflow.com/questions/41326384/re-writing-uid-and-block-0-on-chinese-supposed-to-be-writable-mifare-1k-card-i) pasted the well-known backdoor commands.

## Back door command

There are 2 types of UID writeble cards:

1. Block 0 writable cards: you can write block 0 at any moment
2. Backdoored cards

If writing block 0 does not work, you probably have a backdoored card: To enable the backdoor, you need to send the following sequence to the card: (everything in hexadecimal)

1. RC522 > Card: 50 00 57 cd (HLTA + CRC)
2. RC522 > Card: 40 (7 bits only)
3. Card > RC522: A (4 bits only)
4. RC522 > Card: 43
5. Card > RC522: A (4 bits only)

Then you can write to block 0 without authentication. If it still does not work, your card is probably not UID changeable.