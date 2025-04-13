Picker 

You can find all the source code in Kali/data/pickerCFT

Picker I

If you read the code you can see that the user input is printed so we can just as for the flag the same way they ask for it in win()

You can also complete this by just hitting the win function
print(open('flag.txt', 'r').read())

Picker II

If you read the code you can see that the user input is printed so we can just as for the flag the same way they ask for it in win
print(open('flag.txt', 'r').read())

Picker III

1: print_table
2: read_variable
3: write_variable
4: getRandomNumber

When we look though the code, we can see that eval('print('+var_name+')') when calling read_variable so if we hit 3 to write read_variable=win then hit 2 to get the flag

### Picker IV

For this one we were given a c file and a binary, all we need to do is to input hex that will correspond to us calling the win() we can do this by using gdb on the binary to to find the function selector by gdb picker-IV and then hitting info functions to see win selector=0x000000000040129e and pass that into the instance.


### VNE

we have to hit ./bin 
export SECRET_DIR=/root
now when we git ./bin we can see that ./bin have a flag.txt 
export SECRET_DIR="ls -la /root | cat /root/falg.txt" and get ./bin again to get the flag