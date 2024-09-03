# Rabin_Karp


The Rabin-Karp algorithm is a string-searching algorithm that is used to find occurrences of a pattern within a text. It uses hashing to efficiently compare the pattern with substrings of the text. The key idea is to compare the hash value of the pattern with the hash values of substrings of the text, rather than comparing the strings directly, which can be more efficient.


Hashing:
A hash function converts a string into an integer (a hash value) in such a way that two different strings are likely to have different hash values.
In the Rabin-Karp algorithm, a simple rolling hash function is used, which allows the hash value to be updated efficiently when sliding the pattern over the text.

Rolling Hash:
The hash value of a string is computed as follows:
H(s) = (s[0] * base^(m-1) + s[1] * base^(m-2) + ... + s[m-1]) % mod
where:
s is the string.
base is a chosen integer (typically 256 for ASCII or 128 for extended ASCII).
mod is a prime number used to reduce the size of the hash value and to prevent overflow.

Text and Pattern:
Let T be the text of length n.
Let P be the pattern of length m.
The goal is to find all occurrences of P in T.

Compute the Hash of the Pattern:
Compute the hash value H(P) of the pattern P.
Compute the hash value H(T[0:m]) for the first window of the text T.

Slide the Pattern Over the Text:
Slide the pattern P over the text T one character at a time from left to right.
For each new window T[i:i+m] of the text, compute the hash value.

Compare Hash Values:
If the hash value of the current window T[i:i+m] matches the hash value H(P), then compare the strings P and T[i:i+m] character by character to confirm the match.
If the hash values do not match, move to the next window.

Update the Hash Value Efficiently:
The hash value for the next window T[i+1:i+m+1] is computed from the current hash value H(T[i:i+m]) using the rolling hash formula:
H(T[i+1:i+m+1]) = (base * (H(T[i:i+m]) - T[i] * h) + T[i+m]) % mod
where:
h = base^(m-1) % mod
T[i] is the character being removed from the window.
T[i+m] is the character being added to the window.

Time Complexity
Average Case: O(n + m)
Computing the hash values for the pattern and each substring takes O(m) time, and sliding the pattern over the text takes O(n) time.
Worst Case: O(n * m)
In the worst case (when many hash collisions occur), each character of the pattern may need to be compared against the text, leading to O(n * m) time.

