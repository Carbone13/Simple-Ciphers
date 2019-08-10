# Simple-Ciphers
Simple Ciphers Made Easy

## Shift Cipher

One of the simplest types of encryption is the Shift Cipher. It provides a good introduction to encryption because it is easy to understand.

The Shift Cipher is also called the "Caesar Cipher", because Julius Caesar liked to use it for his personal correspondence. A shift cipher takes the text of the a message and shifts all the letters to to the left or right. For example, if a message was shifted by two, then A would become C, B would become D, C would become E, and so on.

The most popular shift cipher is ROT13 ("ROT" = "rotates"). It shifts letters 13 positions. It is popular because 13 is half of the 26 letter alphabet, which gives it a unique property. The same function can be used to both encrypt and decrypt.

PHP has a built in functio for ROT13 called `str_rot13()`.

    <?php
        echo str_rot13('This is a secret message.');
        // Guvf vf n frperg zrffntr.
        echo str_rot13('Guvf vf n frperg zrffntr.');
        // This is a secret message.
    ?>

There is no built in PHP function for shifting by an arbitrary number, but it is easy to write code for it. Incidentally, Julius Caesar like to use a shift of three.

    <?php
      function str_rot($string, $rot=13) {
        $letters = 'AaBbCcDdEeFfGgHhIiJjKkLlMmNnOoPpQqRrSsTtUuVvWwXxYyZz';
        // "% 26" allows numbers larger than 26
        // doubled letters = double rotated
        $dbl_rot = ((int) $rot % 26) * 2;
        if($dbl_rot == 0) { return $string; }
        // build shifted letter map ($dbl_rot to end + start to $dbl_rot)
        $map = substr($letters, $dbl_rot) . substr($letters, 0, $dbl_rot);
        // strtr does the substitutions between $letters and $map
        return strtr($string, $letters, $map);
      }

      echo str_rot("Experience is the teacher of all things.", 3);
      // Hashulhqfh lv wkh whdfkhu ri doo wklqjv.
    ?>
    
## Substitution Cipher

A shift cipher is actually a primitive version of a Substitution Alphabet Cipher. A substitution cipher uses a translation map for characters. Each character in the text gets translated into another character. The substitution could be into letters, or into numbers or symbols. Decryption simply requires applying the translation in reverse. Decrypting substitution ciphers are popular puzzles to include in newspapers and magazines.

In PHP, the function `strtr()` (short for "string translate") allows mapping one set of characters to another set.

    <?php
      const LETTERS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      const CODEMAP = 'UMRSQPBOLEXTZYAKJVCNHDWGIF';
      function encrypt($string) {
        $uppercase = strtoupper($string);
        return strtr($uppercase, LETTERS, CODEMAP);
      }
      function decrypt($string) {
        $uppercase = strtoupper($string);
        return strtr($uppercase, CODEMAP, LETTERS);
      }
      echo encrypt('TO BE OR NOT TO BE.');
      // NA MQ AV YAN NA MQ.
      echo decrypt('NA MQ AV YAN NA MQ.');
      // TO BE OR NOT TO BE.
    ?>
    
Substitution ciphers are easy to use, but also easy to decrypt. Long messages provide clues because of letter frequency and the particular characteristics of each language. For example, in English, a three-letter word which appears often in a text is probably "the", "and", or "but", and a two-letter word is probably "to", "at", "in", "of", or "is".

These simple ciphers provide basic examples of the principals of cryptography and make it easier to understand more complex examples.
