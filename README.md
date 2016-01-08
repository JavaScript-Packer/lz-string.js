# lz-string.js

Remake &amp; hack of the infamous lz-string. Minified extremely, decode function is less than 1.5KB!

lz-string was designed to fulfill the need of storing large amounts of data in localStorage, specifically on mobile devices. localStorage being usually limited to 5MB, all you can compress is that much more data you can store.

# Is this LZ-based?

Originally an LZW implementation (no more patents on that), which is very simple.

What was manipulated/modded:

localStorage can only contain JavaScript strings. Strings in JavaScript are stored internally in UTF-16, meaning every character weight 16 bits. I modified the implementation to work with a 16bit-wide token space.

I had to remove the default dictionary initialization, totally useless on a 16bit-wide token space.

I initialize the dictionary with three tokens:

An entry that produces a 16-bit token.

An entry that produces an 8-bit token, because most of what I will store is in the iso-latin-1 space, meaning tokens below 256.

An entry that mark the end of the stream.

The output is processed by a bit stream that stores effectively 16 bits per character in the output string.

Each token is stored with just as many bits that are needed according to the size of the dictionary. Hence, the first token takes 2 bits, the second to 7th three bits, etc....
