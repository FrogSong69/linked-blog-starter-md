
Act I

I will skip the first challenge since its just a "how well do you know curl" challenge 

Moving on to Morcel nouget's challenge 

We are told to find a book that is used to crack the note cyhper

The note can be seen here 
![[Pasted image 20241128012839.png]]

If you walk around you will find the book as well as a UV light
The book https://frost-y-book.com/

If you look at the number set up we can make a guess that it will be page:word:letter
This will give us s-a-n-t-a and if we use a phone number to letter system we get a pass code called 72682 which is the correct password! 

This was an Ottendorf cipher

This image we get from out invenotry if we use the script from their hint https://gist.github.com/arnydo/5dc85343eca9b8eb98a0f157b9d4d719 I can reconstruct it but gotta go fast to just turn depending on what you are reading.
![[Screenshot 2024-12-07 at 8.12.53 PM.png]]
now for the wires 
GND on the SLH goes to `G` on the terminal (preferably use a Green jumper wire for this)
VCC on the SLH goes to `V` on the terminal (preferably use a Red jumper wire for this)
Rx on the SLH needs to be connected to the transmitting pin `T` on the terminal
Tx on the SLH need to be connected to the receiving pin `R` on the terminal
The USB Type-C Connector goes on the USB port on the right-hand side of the SLH.
![[Screenshot 2024-12-07 at 8.21.45 PM.png]]