## Awk one-liners

Quickly remove duplicate lines from a single file in place:

`awk '!seen[$0]++' filename`
