# Lab 3
## Part 1
The bug we are use is in the first method, "reverseInPlace". The expected function of this code is to reverse an array in place.

Buggy Program:
```
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

1. Failure Input:
```
  @Test
  public void testReverseInPlace1() {
    int[] input1 = { 1, 2, 3, 4, 5 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 5, 4, 3, 2, 1}, input1);
  }
```
2. Nonfailure Input:
```
  @Test
  public void testReverseInPlace2() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
  }
```

3. Symptoms
   
![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/57ce36c1-8dbf-47ed-89cf-4edc303a7daa)

4. Code Change
   
Before:
```
 static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i++) {
        int val = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = val;
    }
}

```


5.
In the buggy code, the array is not reversed correctly because elements are being overwritten before they can be used for reversal. One fix is to perform our swap (arr[i] = arr[arr.length - i - 1]) but do it with val saving the variable beforehand such that it is not overwritten for the swap on the other side of the array. For example, for 1, 2, 3, 4, 5, if we are on 2, we will set it to 4, but then we also set the 4 in the original array to 2. This also makes it so we only have to traverse half of the array.

## Part 2

`grep` command:

Per the man page, `grep` prints lines that have specified patterns.

EXAMPLE USAGE:

Input File (file.txt)
```
apple
banana
cherry
date
```

| Command Run                                   | Output              |
|-----------------------------------------------|---------------------|
| `grep -i "apple" file.txt`                    | apple               |
| `grep -n "banana" file.txt`                   | 2:banana            |
| `grep -r "cherry" *.txt`                      | file.txt:cherry     |
| `grep -v "date" file.txt`                     | apple<br>banana<br>cherry |

`-i` makes it so the pattern matching is case insensitive.
`-n` displays the line number of the matched line
`-r` does a recursive search of files to pattern match. It returns the file name with the pattern.
`-v` is an inverse pattern match, printing lines that do not have the pattern.


### USAGE IN ./technical

#### grep -i examples:

Input:
```grep -i "conclusion" biomed/1471-2202-3-8.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/54a95d46-64dd-4df5-b843-df87b316c73b)


Input: ```grep -i "hbas" pmd.0020150.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/1e4173d5-1025-4d5c-9cdc-cf10340ef2e3)

grep -i is useful for searching for lines that match your pattern in a non case sensitive way. In the examples above the files are being searched for lines that match the pattern provided, regardless of case. 

Source: man grep

#### grep -n examples:

Input: ```grep -n "med" pmd.0020149.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/fc4a2087-8bfd-45c0-bbcc-90b021141086)

Input: ```grep -n "you" Justice_for_all.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/1d7fbaf5-f413-44c9-abe6-0ff6db596e74)

grep -n finds the line number that the pattern appeared on. This can be useful if you are planning to open the document in a text editor for further editing, as you can navigate to the exact line you want quickly.

Source: man grep

#### grep -r examples:

Input: ```grep -r "you" govenrment```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/ee6dc192-25e3-446b-961d-5d9d962a7a89)

Input: ```grep -r "you" biomed```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/1c8dc6a2-f84a-46bf-bcb5-9a2853f6e221)

grep -r searches recursively through a provided directory for your pattern. It will display the name of the file upon execution. This is useful for looking through a large amount of files, where providing the path for each file with normal grep is not possible.

Source: man grep

#### grep -v examples:

Input: ```grep -v "s" journal.pbio.0030137.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/1e005666-99c7-4f4d-be83-4462206afe61)

Input: ```grep -v "s" chapter-10.txt```

Output:

![image](https://github.com/anngo-1/cse15l-lab-reports/assets/75955073/60215abc-8389-471b-968d-4f86654b9ebc)

grep -v searches for lines that are not the provided pattern. This is useful for filtering out lines if your text file has a consistent pattern (i.e. there is a "2020:" denoting the date on every line, you want to look at entries that are not from 2020)

Source: man grep
