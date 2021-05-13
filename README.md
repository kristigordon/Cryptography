![Alt text](https://coverfiles.alphacoders.com/260/thumb-1920-26096.jpg "Matrix Banner")


# Cryptography

![Alt text](https://th.bing.com/th/id/OIP.SXFyZBXsZQnZZv04TIqQCwAAAA?pid=ImgDet&rs=1 "Hacker small") 
Cryptography is the science of secure communication through the use of codes and ciphers. A
code replaces whole words with other words; a cipher scrambles or replaces the letters in
words (so technically, Morse code is really Morse cipher). One goal of cryptography is to use a key to 
both encrypt readable plaintext into unreadable ciphertext and then decrypt it back to plaintext. 
The goal of cryptanalysis is to decode ciphers and codes without knowing their key or encryption algorithm.

Our project today is based off of the Anson Stager, cofounder of Western Union and head 
of the US Military Telegraph department. He have the Union a huge advantage over the 
Confederacy through his Route Transposition Cipher. This cipher was a combination of real 
words and code words that could be broken down in a matrix. The Route Cipher was one of the 
most successful military ciphers of all time. Let me show you why. 

We will start with this outline of the project:
```
Load the ciphertext string.
Convert ciphertext into a cipherlistto split out individual words.
Get input for the number of columns and rows.
Get input for the key.
Convert key into a list to split out individual numbers.
Create a new list for the translation matrix.
     For every number in the key:
     Create a new list and append every nitems (n= # of rows) from the cipherlist.
     Use the sign of key number to decide whether to read the row forward or backward.
     Using the chosen direction, add the new list to the matrix. The index of each
     new list is based on the column number used in the key.
Create a new string to hold translation results.
For range of rows:
     For the nested list in translation matrix:
          Remove the last word in nested list
          Add the word to the translation string.
Print the translation string.
```
Here is the Cipher:
```
ciphertext = "16 12 8 4 0 1 5 9 13 17 18 14 10 6 2 3 7 11 15 19"
```

Cipher list prints out each element in the list instead of printing '1' then '6' it is '16'. (splits at space)
```
cipher_list = ciphertext.split()
```

```
columns = 4
rows = 5
```
Here, a negative number means read UPthe column, vs. read DOWN the column in a positive interger. 
```
key = '-1 2 -3 4' 
```
A place to store the elements in a string as we decode
```
translation = ''
```
Create a matrix variable to contain a list of 4 items (4 is the number of columns) 

Later on we are going to replace the none values with lists to make a list of lists.
```
matrix = [None] * columns
```
Represents the first index of a list and stop is the number of rows.
```
start = 0
stop = rows
```
Taking the key and iterating through each element and changing it from an str to an int and then seperate each using split on each space. 
```
key_int = [int(i) for i in key.split()] 
```
Now we are going to make the matrix which is shown as a list of lists. Each list is a column of the matrix.
```
for k in key_int:
     if k < 0: #negative number means that we are reading from bottom to top which is the correct order for us. 
         column_items = cipher_list[start:stop]
     elif k > 0: #postive number means that we are readung from top to bottom, we will need to reverse this order.
         column_items = list(reversed(cipher_list[start:stop]))
```
Need to have a indexed list for matrix and need each index to be 0, the value of k can't 
   Then we need to put in a list to replace each 'None' in the matrix.
   For example, the first column [16, 12, 8, 4, 0] replaces the None in the matrix.
    # Matrix[0] = [16, 12, 8, 4, 0] 
    To find 0, we will use k. 
When k is -1, we are on the first item, we take the absolute value using abs function, to get the index of 0.
Next in the key_int, k, will be 2. So taking 2 - 1, we get index 1 which is our next list. And this continues through key_int.

We then want to add the column_items into this spot. 
      ```
      matrix[abs(k) - 1] = column_items
      ```
Now we need to update the values of the start and the stop otherwise, we will continue using the first index through the loop.
     # example : [['16', '12', '8', '4', '0'], ['0', '4', '8', '12', '16'], ['16', '12', '8', '4', '0'], ['0', '4', '8', '12', '16']]
Originally, the start and stop variables were defined by rows, so we now need to add rows to them again to keep iterating through the list. 
     ```
     start = start + rows
     stop = stop + rows
     ```
```
print(matrix)
```
```
Output = [['16', '12', '8', '4', '0'], ['17', '13', '9', '5', '1'], ['18', '14', '10', '6', '2'], ['19', '15', '11', '7', '3']]
```
We iterated through each list, and also reversed the 2nd and 4th so that it is easier to decode. 

You should now be able to easily decrypt a route transposition cipher with a known key or
test suspected routes by using the script’s clear and accessible interface to adjust the key.


![Alt text](https://th.bing.com/th/id/R58c1980a42ebad7d994cc62f90a5d7d8?rik=vQR%2bYTG6VW3I5Q&riu=http%3a%2f%2fecx.images-amazon.com%2fimages%2fI%2f41MAP2TotSL._SY300_QL70_.jpg&ehk=57kf8Zxs7DpviMiiQ4E9IINxfkHGhhnXz3YnsKxjA9U%3d&risl=&pid=ImgRaw "Warning") 
This project contained some basic elements decoding and encrpyting. 

# Please, use your powers for good. 

![Alt text](https://www.securemac.com/wp-content/uploads/2017/03/AdobeStock_123396196.jpeg "Hacker")
