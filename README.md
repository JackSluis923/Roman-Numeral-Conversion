# Roman-Numeral-Conversion

## Code ::

# Converting from arabic -> roman:

roman = {1000: "M", 
         900: "CM", 
         500: "D", 
         400: "CD", 
         100: "C", 
         90: "XC", 
         50: "L", 
         40: "XL", 
         10: "X", 
         9: "IX", 
         5: "V", 
         4: "IV", 
         1: "I"}

ret = ""

num = int(input("Enter a number"))
store = num

for key, value in roman.items():
    for k in range(int(num/key)):
        ret += value
        num -= key
        
print("Converted number (from " + str(store) + ") - " + str(ret))

# Converting from roman -> arabic:

import re

conv = {'I' : 1, 'V' : 5, 'X' : 10, 'L' : 50, 'C' : 100, 'D' : 500, 'M' : 1000}
numRe = re.compile(r'(\w){1,10}')

numeral = input("Enter a Roman Numeral")
ret = list(numRe.search(numeral).group())
countDict = {}
for i in range (len(ret)):
    count = 0
    for c in range (len(ret)):
        if (ret[c] == ret[i]):
            count += 1
    countDict.setdefault(ret[i], count)
    
print(ret)
print(countDict)
    
for value in countDict.values():
    try:
        assert(value <= 3)
    except:
        raise Exception ("You can't have more than 3 of any roman numeral you dingus")
    if ('V' in countDict.keys()):
        if (countDict['V'] > 1):
            raise Exception ("Roman numerals V, D, and L can't be repeated (represented by other roman numerals)")
    if ('D' in countDict.keys()):
        if (countDict['D'] > 1):
            raise Exception ("Roman numerals V, D, and L can't be repeated (represented by other roman numerals)")
    if ('L' in countDict.keys()):
        if (countDict['L'] > 1):
            raise Exception ("Roman numerals V, D, and L can't be repeated (represented by other roman numerals)")

fin = 0

k = 0
for k in range (len(numeral) - 1):
    print(numeral[k])
    if (conv[numeral[k]] < conv[numeral[k + 1]]):
        fin += conv[numeral[k+1]] - conv[numeral[k]]
        if (countDict[numeral[k]] > 1):
            countDict[numeral[k]] -= 1
        else:
            countDict.pop(numeral[k])
        if (countDict[numeral[k+1]] > 1):
            countDict[numeral[k+1]] -= 1
        else:
            countDict.pop(numeral[k+1])
            
for key, value in countDict.items():
    fin += conv[key] * value
    
print(str(numeral) + ' - ' + str(fin))
