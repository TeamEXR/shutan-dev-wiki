# Text and Localization

gflib_cpp, GameFreak's internal core framework for games, supports specialized text archives for games. The code for this is largely based on the same code used for text archives in gen 3, 4, and 5 before getting abstracted into GF's game engine as the `gfl::str` namespace.

These text archives support:

- Multiple versions of the same text line, intended for multiple language support.
- Encryption of the text to avoid important info leaking out early (gen 3 to 6 games shipped with event pokemon already supported in-game, text archives were encrypted to avoid details of these pokemon leaking before they were distributed)
- Custom tags that can query the game for info (such as the player's name or their party's lead pokemon) or tell the game to format the text (such as coloring the text and changing the font size)

> The gen 6 games actually separate text by their language and store them in separate GARCs. It seems like the text archive format's multi-language support is only used to store the Hiragana and Kanji versions of the Japanese text together [TODO: ask a Japanese guy to confirm this]

[TODO: Write down the algorithm used for decryption/encryption of the text as well as the algorithm for tags used in the gen 6 games]

## gflib text archive format

Each text archive is divided into multiple sections based on the number of languages/handwritings used. Then each section stores a series of text lines. The header consists of a main part and a number of smaller parts specifying line info and section info

```c++
struct TextArchiveHeader{
    /*0x00*/ uint16_t sectionCount;                 // number of sections
    /*0x02*/ uint16_t lineCount;                    // number of lines in the archive
    /*0x04*/ uint32_t maxSectionSize;               // size of the biggest section in the archive
    /*0x08*/ uint32_t isEncrypted;                  // == 0 if encrypted, == 1 if not
    /*0x0C*/ uint32_t sectionOffsets[sectionCount]; // offsets to the start of each section (counted from the start of the file in bytes)
}; // size = 0x10

struct TextArchiveSectionHeader{
    /*0x00*/ uint32_t size;                                          // size of the section in bytes
    /*0x04*/ TextArchiveLineInfo lines[TextArchiveHeader.lineCount]; // array of info about each line
};

struct TextArchiveLineInfo{
    /*0x00*/ uint32_t offset;  // offset to the start of the line string
    /*0x04*/ uint16_t length;  // number of characters in the line string (including EOM)
    /*0x06*/ uint16_t unknown; // unknown field, always 0
} // size = 0x0C
```

>  lines of text in text archives only end with EOM, not with `\n`. This is because `\n` is used to let messages in gen 6 games support multi-line text.

> The strings are stored using wide characters, meaning that each character of a string takes two bytes.

## how to encrypt/decrypt gflib text files

Set up the key for encryption/decryption (This key is `(0x2983 * (stringIndex + 3))` in gen 6 games), then iterate over each character of the string. On each iteration:

1- XOR the character's binary form with the key. If the character is encrypted this will decrypt the character. If the character is decrypted it will be encrypted.

2- Bit rotate the key right 13 times

```cpp
void decryptOrEncryptGFLibTextString(wchar_t* string, uint32_t stringLength, uint32_t stringIndex, wchar_t* destination){
    uint16_t mask = static_cast<uint16_t>(stringIndex); // clamp the stringIndex to two bytes to avoid side effects
    mask = (0x2983 * (mask+3)) & 0xffff; // the "& 0xffff" clamps the mask to two bytes again in case the compiler messes up the casting
    for(int charIndex = 0; i < stringLength; ++i){
        wchar_t currentChar = *(string + charIndex);
        currentChar ^= mask;
        *(destination + charIndex) = currentChar;
        mask = ( ( (mask & 0xe000) >> 13) | ( (mask & 0x1fff) << 3) ); // rotate the mask right by 13. the additional ANDs are there to discard any unneeded bits
    }
}
```

## Tags

The `gfl::str` system supports custom Tag codes that can either format the text (e.g. color it) or more commonly query the game for information and put it in the text. For example you can use a tag to get the player's name or their lead pokemon's name.

Tag codes are implemented as a special binary sequence. First a special code signifies the start of a Tag sequence (let's call it TAG_START), the next byte then signifies the number of tags and their arguments in the tag sequence. then the tags follow with their arguments after their tag code.

For example, if you write this:

```
Hi! this text is TAG_START 2 TAGCODE_COLOR 2 Blue! TAG_START 2 TAGCODE_COLOR 1 But this text is Red!
```

And swap out the tag codes for their actual value (TAG_START = 0x10, TAGCODE_COLOR = 0xFF00)

```
Hi! this text is 0x10 2 0xFF00 2 Blue! 0x10 2 0xFF00 1 But this text is Red!
```

It would turn into this:

[TODO: insert XY text example screenshot here]

You can pair up tags together for fancy stuff

[TODO: insert example of calling out the trainer using colored text here]

[TODO: add a table showing every available tag and their arguments here]