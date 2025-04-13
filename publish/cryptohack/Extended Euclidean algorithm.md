
The **Euclidean algorithm is a way for us to get the GCD of a pair of numbers**

gcd(428, 22)

428 = 22(19) + 10

22 = 10(2) + `2`

10 = 2(5) + 0

So the gcd is 2 we when we get a value to be + 0 at the end

liniear combination

every pair of positive intergers’ gcd have a liniear combination

We use the Extended Euclidean algorithm to find the a liniear combination of the initial two numbers

gcd(428, 22) = 2 work backwards

2 = 22 - 10* 2

2 = 22 + 10* -2

2 = 22 + (428-22* 19)_-2

2 = 22 + (428 + 22* -19)*-2

2 = 22 + ((428* -2)+((22* -19)* -2)

2 = 22 + ((428* -2)+(22* 38)

2 = (22* 39) + (428* -2)