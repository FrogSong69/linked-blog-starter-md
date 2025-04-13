
When we break a mod into different values we need to make sure that the GCD is 1

x ≡ r1 (2) mod 5  
x ≡ r2 (3) mod 11
x ≡ r3 (5) mod 17

Example here the GCD(5,11) = 1 GCD(5,17) = 1 GCD(11,17) = 1 which mean we can use it.

the above show case that m = 935 since that is the product of multiplying all the mods

Note there that we can find mi for each by doing m1 = m/m1 - m1 here being the first mod congruent in this case 5 so m1 = m2 * m3 same can be applies to the others.

m1 = m2 * m3 
m2 = m1 * m3 
m3 = m1 * m2 

Then we have a value corresponding to each mi called xi

with all of that we can then calculate the product by xi * mi * ri 

x1 * m1 * r1 
x2 * m2 * r2 
x3 * m3 * r3

Then we will take the sum of all 3 and that will give us x

Now lets find xi 

To find the inverse of x1 ≡ r1 (2) mod 5 we need to corresponding m1 which is 187

187x1 ≡ 1 (mod 5)
2x1 ≡ 1 (mod 5) meaning x1 = 3

To find the inverse of x2 ≡ r2 (3) mod 1 we need to corresponding m1 which is 187

85x2 ≡ 1 (mod 11)
8x2 ≡ 1 (mod 11)
Use the Extended Euclidean Algorithm:
1 = 3 * 11−4 * 8 ⇒ −4 * 8 ≡ 1 (mod 11)
−4x2 ≡ 7 (mod11) = 7

55x3 ≡ 1 (mod 17)
4x3 ≡ 1 (mod 17)
−4≡13(mod17)
x3≡13(mod17) = 13

5734