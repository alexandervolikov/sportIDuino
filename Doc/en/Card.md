This development branch is devoted to the use of common chips Mifare Classic 1K (S50). They come bundled with the RC522 module, and can also be purchased separately. Their structure is noticeable different from Ntag chips, especially the implementation of encryption, so incompatibility occurs and requires the use of separate firmware for base stations and master stations. For the convenience of developers, the structure copies Ntag, leaving three-quarters of the memory unused.

The chips S50 can record up to 42 marks, in the form of key fobs, these chips cost 10 rubles. You can significantly increase the capacity of chips (up to 170 marks), but this is fraught with the risk of data loss, since you will have to have several marks on one page, which involves the risk of data loss, as the record is performed only in whole pages.

![](https://raw.githubusercontent.com/alexandervolikov/sportiduino/master/Images/Chip.JPG)

The structure of the record is below. It is copied from the description for Ntag. The difference from Ntag213 is that it is used for 10 pages more. For a better understanding of the differences, please refer to [datasheet] (www.nxp.com/documents/data_sheet/MF1S50YYX.pdf)

The structure of the record is presented below. 4-7 pages are reserved, the rest of the pages are for the mark. In the 4th page, the first two bytes contain the programmable card number. The third byte contains information about card type: 3 - Ntag213, 5 - Ntag 215, 6 - Ntag 216, it is automatically set. In the 4th byte, the firmware version. On the fifth page, the initialization time of the card in unixtime format (with it you can restore the first byte time in the marks.) Then two pages of the reserve. The recording of a mark on the station takes a separate page, the first byte of which records the station number, in the remaining three bytes - the lower bytes of the current time in unixtime (the total time is then restored using the initialization time recorded in the 5th page ).

![](https://raw.githubusercontent.com/alexandervolikov/sportiduino/master/Images/Ntag2.JPG)

The cards for programming stations have a different structure. The station recognizes them by the number 255, recorded in the third byte of the 4th page. There are 5 different master cards: time, numbers, sleep, settings and dump. Below is their structure. After reading them, the station performs the function set in them and erases them in order to prevent accidental reuse.

![](https://raw.githubusercontent.com/alexandervolikov/sportiduino/master/Images/Master-Ntag2.JPG)