# Noisy

So i averaged the first 10 nums and gave it a number as well as add 0.5 (to reverse what the source did) this gave me binary and i replaced it with values from source. i shoved it into a morse code decoder to get a pattern and then brute forced the flag by guessing what the letters could be
```python
import numpy as np
from random import gauss
import math

out2 = "100100101101000011011011000010100001010000001101011011000011010010010110110000101000010101000010111100001101000011011011000111100001010000101101010011000011010000110100110000100000010101000010101100001101000011011011000010100001010100000111011011001010010001110110110000101100110101000010101100001101000011011011000010100001010100001101011011000011010000110110110000100000010101000010101100000011100011111011000010000001010100001101011011000011010100110110110000101000010101010010111100001100000011011110000010100011010100001101011011001011110000010110110000101000010101000010101100011101000011011011000010100001010110001100011011000011010100111010110001101000010101000010101100001101000011011011000010100001010110001101011011000011010000110110111010101010010101000010101110001101000011010011000010100001010100001101011011000011010000110100110000101000010101000010101100001101000011011011000010100001010100001111011011100011010000101110110000101000010101000010101100001101000011011011000010100011010100101101011011000011110000110100010000111000010101000010101000001101010011011011000010100000010100000101011011000011010000110110110000101000010101000010101000001101000011011011000010100001010100001101011011000011010000110110110000101000010101000110101100001101010011011111000010100001010100001101011011000001110000110110110000101001010101001010101100001001001011011010000010100001010101001101011111000011010100010110110000101000010101000010101100001101000011011011001010000000010100001101011011000011010000110110110000101000010101000010101100001101100011011011010000110001010000001101011011000011010000110110110000101000010101001011101100001101000011011010000010100001010101001001011011000011011000110110010000101001010101000010101100001111000011011011000010110001010100101101011011000011010000110110111000101000010100000010101100001101010011011011000010100001010100001101011011000011011000110110110001101000011101001010101100001001000011011011000010100010010100001101011011000011010000110100100000101000010101000010111100001101000111011011000010100001010100001101011001000011010000110110110000101000110101000000101100001101010011011011001010101001010100001101111011000011010000110110110000101000010111000010101100001101000011011011000010100001010100011101011011000011010001110110100000101000010101000010101100001101000011011011000010100101010100001101011011000011010000110110110000101000000101000010101110001101000011011111000110100001010100001101011011000011010000110110110000001000011000000110101100000101000011011011000010100001010100000101011011000011010100110110110000101001010100001010101100001101000011011001000010101011010100001101011111000011010000110010110000101000010101000010100100001101000011011011001010100001010100001101011111000011010000110110100000101010000101000010101100001101000011111011000000110001011100001111011011000011010000011110110000101000010101000010"
out = []
out2 = ""
with open("flag.txt","r") as f:
	cont = f.read().split("\n")
	sums = 0

	for i,num in enumerate(cont):
		sums += float(num)
		sums += float(cont[i+14400])
		if (i + 1)%10 == 0:
			out.append(sums/20+0.5)
			sums = 0
		if i == 14399:
			break

for i in out:
	a = round(i)
	if a < 0:
		a = 0
	if a > 1:
		a = 1

	out2 = out2 + str(a)

print(out2)	

"""
10010-11012010000110110110000101000010100000011010110120000110100100101101100002010-10010101000010111100002102000011-111011000111100001010000101101020011000011010000210100110000100000010101000-110101100-102201000011011-111-1-100101000-110201000-101120120110010200100011101101100002011001101020000101011000-111010000120110210000101000010101000011010110110000110100001101101100001000000101-110000101011000000111000121110110000100000010101-10001101-111011000011-1101001101101100-101010-100101-1101001011120000110000-1-111011110000-11010001101010000110201102100101111000001011011000-1101000-11010100-1010101100012101-100011011012000020100001010110001100011011000011-11010-1111020110-10110100001010100001-1101100001101000011011011000010100001010110001102021011000-1110100-1011011011101010101001010100001010111-10-1210100001101001100001-110000101010000110101101100-1011010000110100110000101000010101-1000201011000011-11-1000110110110000101000010101000011110120121000110100-1010122011000-11010-10020101000-1101011000011-1100-1011011011000010100011010100101101011011000011110000110100020000111000010101000-1102010000011010100110110110000101000000101000001010110110-10011-11000011011011000010100001010100001010100-1001101000011011011000010100001-1101-1000110101101100001101000011021011-10-1010100001010100011-1101100001101010011011111-10-1010100001010100001101011-111000001120000110110110000101001010101001010101100002001001011021010000010100001010101001101011111000012010100010110110000101000010101-1000101012000011010-10-11101101100101000000001010000110102101100001101000011011011-100-110100002010100001010110000110110001101101101-1000110001010000-1011010110110000110100001201101100001010000101010010111011-10-10110100001101102000-1-110100001010101001001011-1110000110110001101100100001010010101010000101011000011110000110110120000101100020101001011010110110000110100001101101110002010000102-1000002010110000110101001101101100001010000101010000210101101100001202100011011011000110100001110200101010110000100100001101101100001-11000100101000012010110110000110100002101001000001010000101010000101111000011010001110110110-1001010000101010000110101100100001101-1000110110110000101-1001101-110-10000201100001101010011021-111001010101001010100001101111011000011-1100001101101100002010000101110000101011000011010000110110110000101-1000101010001120101101100001101-10011101101000-10101000010101000010101100001101-100011022011000010100101010100001101021021000011-11000011011011-100020100000-1101000010101110001101000-121011111000110100002010100001101011011000011010000110110110000001000011000000110101100000101000011011011-1000101000020101000-10101011011-1-100110101002101101100001010010201000010101-11100001101000011011001000010101011-11010000210101111100001101000011001011-1000101000010101000010100200001101000-121011011001010100001010100001101021111000-11101000011011010-10001010100001010-10010101100001101000011111011000000110-10101110-1-10111102102100001101000001111011000010100001010100001-1"""
print(len(out2))

out3 = out2
out4 = out3.replace("110","-")
out4 = out4.replace("000"," ")
out4 = out4.replace("10",".")
#out4 = out4.replace("00","")
out4 = out4.replace("0","")
out4 = out4.replace("1",".")
print("---------")
print(out4)
input()
```