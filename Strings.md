## String Hashing

We can efficiently check string equality by comparing the hashes for the two strings. The idea here is to caluclate the hash values for each character in the string

 
 **(sum (ASCII value * Constant<sup>position</sup>)) mod OtherConstant**
 
 
 where "Constant" and "OtherConstant" are pre-chosen and should be randomly chosen near 10<sup>9</sup> so as to better avoid collisions (there are more string possibilities than hashing values, so collisions are possible).

 ### Benefits

Consider this problem: Given a string *s* and some pattern *p*, find the positions where *p* occurs in *s*. A brute force approach to this problem would take O(n<sup>2</sup>) time. Instead, by using hashing, each check for equality does not go through each character, and instead is done in O(1) time. This approach could then ultimately bring the time complexity down to O(n).