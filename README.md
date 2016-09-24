# NAME

Text::Shinobi - 忍びいろは (Ninja Alphabet) encoding

# SYNOPSIS

    use Text::Shinobi qw/shinobi/;

    print shinobi('しのび'); # => 𨊂浾⽕紫゙

# DESCRIPTION

"Shinobi Iroha" is a method to encrypt message that Ninja used.
This substitution cipher map the Japanese Kana characters to Kanji.

Text::Shinobi encoding table is based on 萬川集海 the Ninja technique encyclopedia; compiled in 1676.
The exact character table has not been revealed in the book (as strictly confidential).
This module adopted table "generally known" in current Ninjalogy.

# METHODS

## encode()

    Text::Shinobi->encode('あいう！'); # 𣘸栬𡋽！

Returns encrypted input text (unicode string).
Only Hiragana and Katakana are converted, other characters are left.

### $Text::Shinobi::ENCODE

By default, `encode()` select a Kanji character following rules:

1. use single character if same shape unicode exists.
2. viewable in a common (in 2016) browser fonts.

So this module's default might change in the future.

You can change encode option by `$Text::Shinobi::ENCODE` class variable with below constants.

    # DUO: double character only
    local $Text::Shinobi::ENCODE = Text::Shinobi::DUO;
    Text::Shinobi->encode('あいう'); # => ⽊黒⽊⾊⼟⾚

    # UTF8MB3: exclude 4 bytes code as utf-8
    local $Text::Shinobi::ENCODE = Text::Shinobi::UTF8MB3;
    Text::Shinobi->encode('あいう'); # => ⽊黒栬⼟⾚

## decode()

    Text::Shinobi->decode('𣘸栬𡋽？'); # あいう？

Returns text to try decode input text (unicode string).

# EXPORTS

No exports by default.

## shinobi()

    use Text::Shinobi qw/shinobi/;

    shinobi('...');

Shortcut to `Text::Shinobi->encode(...)`.

# ADVANCED USAGE

Romaji to shinobi iroha: use [Lingua::JA::Kana](http://search.cpan.org/perldoc?Lingua::JA::Kana);

    use Lingua::JA::Kana;

    shinobi(romaji2hiragana('ninja!'));

# AUTHOR

Naoki Tomita aka "Tomimaru" <tomita@cpan.org>

# LICENSE

Copyright (C) Naoki Tomita.

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.
