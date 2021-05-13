# Cryptography

Cryptography is the science of secure communication through the use of codes and ciphers. A
code replaces whole words with other words; a cipher scrambles or replaces the letters in
words (so technically, Morse code is really Morse cipher). 

One goal of cryptography is to use a key to both encrypt readable plaintext into unreadable 
ciphertext and then decrypt it back to plaintext. The goal of cryptanalysis is to decode 
ciphers and codes without knowing their key or encryption algorithm.

Our project today is based off of the Anson Stager, cofounder of Western Union and head 
of the US Military Telegraph department. He have the Union a huge advantage over the 
Confederacy through his Route Transposition Cipher. This cipher was a combination of real 
words and code words that could be broken down in a matrix. The Route Cipher was one of the 
most successful military ciphers of all time. Let me show you why. 

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
# We iterated through each list, and also reversed the 2nd and 4th so that it is easier to decode. 
