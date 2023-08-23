# PAK - Vib-Ribbon Archive

Vib-Ribbon's PAK format is the primary data storage structure in the game. Compared to other propietary formats of archival from other games, this one is relatively simple. Several of them are laid throughout the game files. Unlike the usual ZIP, 7Z, or GZIP file, the contents are stored uncompressed, akin to a TAR archive, little endian. Of course, the files inside are indexed with a basic table of contents.

## File Makeup

| Header | File Offset Table | File Name | File Length | File Data |
|:------:|:------------:|:----------:|:--------:|:-------:|

*(The last three are run through for each file that exists in the archive.)*

The short rundown of what each of the parts of the file do.

* The header, being only four bytes long, contains just the file count in the archive, stored as an unsigned integer, which can potentially carry up to 4.2 billion files inside... not that you'd want to though.
* There is also a series of offsets that the game creates pointers for that denotes the correct place where the beginning of the file should be. This is known as the offset table, also known as the "table of contents."
* At each file offset, the file name is given first, including the directory. If the number of characters in the file name is not a multiple of four, there can be 1 to 3 null characters that pad to the next 4-byte sequence, which contains the length of the file in bytes, as an unsigned integer. Finally, the file data itself is placed after.

## PAK Implementations
### FILES.PAK and xx_FILES.PAK
The PAK files for vib-ribbon are placed under `GAME\`, `TITLE\`, and `KIOSK\`, which are then used by their respective executable, and are unpacked during gameplay.

In the Japanese game, all PAK files are named `FILES.PAK`, which cannot be said for the European version, because of the presence of multiple languages. Each language has a prefixed number at the beginning of its filename, and is written in base-16, double for each language. Some of the files contained also have this prefix, depending on whether there is translated text or not.

* `01_FILES` - Japanese
* `02_FILES` - English
* `04_FILES` - German
* `08_FILES` - Spanish
* `10_FILES` - French
* `20_FILES` - Italian

`TITLE\FILES.PAK` maintains the same name in the Japanese and European releases of vib-ribbon. Its translations are also included in the same directory as the file that is translated, because MAIN\_T is able to change the language on the fly, whereas the setting is only carried over to MAIN\_G and MAIN\_K.
