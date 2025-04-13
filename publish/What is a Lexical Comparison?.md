
A **lexical** (or **lexicographical**) comparison is like comparing words in a dictionary — character by character, left to right.

---

## 📜 JavaScript Rules for Lexical String Comparison
When you compare strings in JavaScript using `<`, `>`, `<=`, `>=`:

1. JavaScript **does not** look at the value of the number the string might represent.
    
2. It compares strings **one character at a time** using their **Unicode code points**.
    
3. The first pair of characters that differ determine the result.
    
4. If all characters are the same but one string is longer, the shorter one is considered smaller.


Reason why 

'+100' < '1' is because of rule 3 and we dont use rule 4 here

so since signs are lower unicode than numbers this is true
and if we consider 'a100' < '1'  that does not work because letters are higher unicode than numbers same as '100000' < 'z' would be true