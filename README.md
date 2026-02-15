# wpspin-dict
WPS PIN Dictionary for Hashcat

## Why use hashcat when reaver exists?

Yeah it's only 11000 combinations but you're gonna get locked out after the third.

That doesn't mean that WPS is useless though. Some router brands(TP-Link for example) use WPS PIN as a default WPA2 PSK password so that you can "look for the password on the back of the router".

The naïve approach is to use a mask. ?d?d?d?d?d?d?d?d is 10^8 combinations(~5 mins on GTX1660S or ~50 mins on Vega 7) but the last digit of the PIN is a checksum so there's only 10^7 valid PINs.

WPS_PIN = d1 d2 d3 d4 d5 d6 d7 C

C = (10 - (S % 10)) % 10

S = 3*(d1 + d3 + d5 + d7) + (d2 + d4 + d6) 

di ∈ {0..9}

Weights pattern: 3 1 3 1 3 1 3 1

Simply put 3*(d1 + d3 + d5 + d7) + (d2 + d4 + d6 + d8) is always a multiple of 10

In practice using this dictionary leads to a 5x decrease in time needed to crack the password. Not 10x because you don't use your GPU as a multiplier.
