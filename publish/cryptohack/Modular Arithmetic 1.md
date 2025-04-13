A find fact is that we use modular arithmetic every time we look at the clock (mod 12)

13 % 12 = 1 (pm)
5 % 12 = 5 (am)
...1

 is that when we divide the integer aa by mm, the remainder is bb. This tells you that if mm divides aa (this can be written as m∣am∣a) then a ≡ 0 mod m, a ≡ 0 mod m.


a ≡ b mod m
I the below where we want to find x we can do that by saying a % m = b
11 ≡ x mod6

Find the modular inverse

We can see that we are solving for D in this case and we can do this by first doing using the 

- **Check gcd**: Verify gcd⁡(a,m)=1\gcd(a, m) = 1gcd(a,m)=1 using the Euclidean Algorithm (inverse exists if gcd = 1).
- **Apply Euclidean Algorithm**: Divide repeatedly to reduce mmm and aaa until r=1r = 1r=1.
- **Work backwards**: Use the equations to express 111 as a⋅x+m⋅ya \cdot x + m \cdot ya⋅x+m⋅y (Extended Euclidean Algorithm).
- **Extract inverse**: The coefficient of aaa (from Step 3) is the modular inverse.
- **Make positive**: If negative, add mmm to get a positive result.


$$
5⋅d≡1 (mod 17)
$$
$$
1 = (5*-3) mod 17
$$
$$
−3 (mod 17)=17−3=14
$$