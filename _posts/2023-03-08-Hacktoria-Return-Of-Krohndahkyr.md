---
title: HACKTORIA - Return of the Krohndahkyr
author: Jose Suarez
date: '2023-03-07 11:05:45 +0200'
categories: [hacking, hacktoria, ctf]
tags: [Hacking, OSINT, Cipher, Hacktoria, CTF, flags]
img_path: /assets/posts/contracts/
---

# Mission Briefing

We are using the codename K; I believe it stands for Cat in my regular Alias; Control typically makes jokes with it; they're not as serious as I wish them to be; I'm here on the field performing these missions for them facing aliens and other things; can't they get my codename right?

Anyways, It appears that the Krohndahkyr have returned after all. Area 51 reported seeing a Space Marine landing craft in the Amazonas region, close to Brazil. However, the Amazonas region is a HUGE one, so I'm not sure how Area 51 can keep track of everything there.

As per usual the US Spaceforce is out of combat and now it's the big guys turn to play. Lucky for me General Rodriguez is willing to allow me to go there, He said some old school movie line, not that i dislike it, some find it cringe, but i actually used some cool lines before.

Just as I was getting ready to battle in the Jungle Rambo style with these Predator creatures, they informed me I needed to go to Sardinia, Italy, to translate some old runes. I mean, I know I'm a genius, but doesn't Control have a special unit for this type of thing?

But hey, it's either fly to Italy, do a quick job, take a break at Rome, or train the new guy, gosh I hate this Agent P.

![Krohndahkyr](https://hacktoria.com/wp-content/uploads/2023/01/Krohndahkyr-cover.png)
_Krohndahkyr portrait, ughh they're ugly!_

* Contract URL: [Return of the Krohndahkyr - Hacktoria](https://hacktoria.com/contracts/return-of-the-krohndahkyr/)
* Faction URL: [Krohndahkyr - Hacktoria](https://hacktoria.com/krohndahkyr/)
* Objetive: Decipher the text in the plaque, get the password to the .zip file and get safely back home for another mission.

# On the field

Control gave us some clues that we can check in the Faction: [Krohndahkyr - Hacktoria](https://hacktoria.com/krohndahkyr/) section of the website.

Some clues:
* The trident/fork is the **letter K**
* They were here between 30BC ~ 210AD
* They for some reasons like Earth and take vacations here, for ehm *Research*...
* Some pictures with the runes on them, you can tell they're a Pot, a Sword, a Man, a Fire and Wine, if the runes mean the same as in English, you can pretty much see that we actually know that some runes are indeed a letter, like the rune of a trident that's a K.
* An alphabet, which is pretty much like our regular alphabet, abcde...

Armed with this knowledge I fired up Paint and tried to match the alphabet to the English one, and we have something like this:

![alphabet](alphabet.png)
_Yellow: our alphabet, Blue: the known letters, Red: little mistakes, ignore_

Regular ABC and below some of the letters we know...

With the help of the best programming language ever Perl, we can create a script to decipher the ancient text.

Perl script:

```perl
#!/usr/bin/perl

# Define the original and substitute letters
my %substitution_dict = (
    'A' => '?',
    'B' => 'P',
    'C' => 'W',
    'D' => 'O',
    'E' => 'E',
    'F' => 'I',
    'G' => 'R',
    'H' => '?',
    'I' => 'T',
    'J' => '?',
    'K' => '?',
    'L' => '?',
    'M' => 'F',
    'N' => '?',
    'O' => 'D',
    'P' => 'K',
    'Q' => 'S',
    'R' => '?',
    'S' => 'A',
    'T' => '?',
    'U' => 'N',
    'V' => '?',
    'W' => '?',
    'X' => '?',
    'Y' => 'M',
    'Z' => '?'
);

# Get the input string from the user
print "Enter a string to substitute letters in: ";
my $input_string = <STDIN>;
chomp $input_string;

# Create an empty output string
my $output_string = "";

# Iterate through each character in the input string
foreach my $character (split //, $input_string) {
    # Check if the character is a letter
    if ($character =~ /[A-Za-z]/) {
        # Get the substitute letter from the substitution_dict
        my $substitute_letter = $substitution_dict{uc $character};
        # Add the substitute letter to the output string
        $output_string .= $substitute_letter;
    } else {
        # Add the non-letter character to the output string
        $output_string .= $character;
    }
}

# Print the output string
print "$output_string\n";
```

Now we need a sample from the text, lucky the final line is short and have some of the known letters, we transcribe it to our ABC and we get: *YSGFDQFUEQQE*

```bash
# perl poc.pl
Enter a string to substitute letters in: YSGFDQFUEQQE
MARIOSINESSE
```

Good! now we can use our Google-Fu, and we get some Latin books.

Now we have the Book name and the Author.

Now we have a little problem, some PDF give me similar names but with a letter changed, maybe he/she was known with other names or was written bad, anyways why bother trying 10 combinations in 1 minute, when i can spend 1 hour creating a custom Perl script that will do it for me, right?

Format is: *name-of-author-name-of-the-text*

```perl
#!/usr/bin/perl

use strict;
use warnings;
use Archive::Zip qw(:ERROR_CODES);

use constant AZ_PASSWORD_WRONG => 51;

my @words = qw(word word word word word word);

my $zipfile = "flagfile-rotkr.zip";
my $success = 0;

foreach my $word1 (@words) {
    foreach my $word2 (@words) {
        foreach my $word3 (@words) {
            my $password = "$word1-$word2-$word3";
            my $zip = Archive::Zip->new;
            unless ($zip->read($zipfile) == AZ_OK) {
                die "Error reading $zipfile: $!";
            }
            if ($zip->extractTree('', undef, $password) == AZ_OK) {
                $success = 1;
                print "Password is: $password\n";
                print "[+] Successfully extracted $zipfile\n";
                last;
            } elsif ($zip->error =~ /password/i) {
                print "Wrong password: $password\n";
            } else {
                die "Error extracting $zipfile: " . $zip->error;
            }
        }
        last if $success;
    }
    last if $success;
}
print "Failed to unzip $zipfile\n" unless $success;

```

We can now use the password to unlock our card flag and GG.

> Agent Alleycat OUT, i'll be offline for a few days enjoying Rome.
{: .prompt-danger }
