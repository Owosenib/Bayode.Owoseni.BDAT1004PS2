QUESTION 1


```python
Consider the following Python module:

a = 0

def b():

global a

a = c(a)

def c(a):

return a + 2

After importing the module into the interpreter, you execute:

>>> b()

>>> b()

>>> b()

>>> a

?

What value is displayed when the last expression (a) is evaluated? Explain your answer by indicating what happens in every executed statement.
```

SOLUTION 1

a = 0
def b(): 
 global a
 a = c(a) 
def c(a):
 return a + 2 
 
 
//Explanation
Every steps 2 is added
 
b() then a is 0 + 2 = 2
 
b() then a is 2 + 2 = 4
 
b() then a is 4 + 2 = 6
 
a was eventually 6


![image-2.png](attachment:image-2.png)



QUESTION 2

Function fileLength(), given to you, takes the name of a file as input and returns the length of the file: >>> fileLength('midterm.py') 284 >>> fileLength('idterm.py') Traceback (most recent call last): File "<pyshell#34>", line 1, in <module> fileLength('idterm.py') File "/Users/me/midterm.py", line 3, in fileLength infile = open(filename) FileNotFoundError: [Errno 2] No such file or directory: 'idterm.py'

As shown above, if the file cannot be found by the interpreter or if it cannot be read as a text file, an exception will be raised. Modify function fileLength() so that a friendly message is printed instead: >>> fileLength('midterm.py') 358 >>> fileLength('idterm.py') File idterm.py not found.

SOLUTION 2

import os



#function to check length of file

def fileLength(file_name):

  try:

    length = os.path.getsize(file_name)

    return length

  except FileNotFoundError:

    #return file not found string

    return "File "+file_name+" not found."

     

#call function to print size

print(fileLength('idterm.py'))  

![image.png](attachment:image.png)



QUESTION 3

Write a class named Marsupial that can be used as shown below: >>> m = Marsupial() >>> m.put_in_pouch('doll') >>> m.put_in_pouch('firetruck') >>> m.put_in_pouch('kitten') >>> m.pouch_contents() ['doll', 'firetruck', 'kitten']

Now write a class named Kangaroo as a subclass of Marsupial that inherits all the attributes of Marsupial and also:

extends the Marsupial __init__ constructor to take, as input, the coordinates x and y of the Kangaroo object,
supports method jump that takes number values dx and dy as input and moves the kangaroo by dx units along the x-axis and by dy units along the y-axis, and
overloads the __str__ operator so it behaves as shown below.
>>> k = Kangaroo(0,0) >>> print(k) I am a Kangaroo located at coordinates (0,0) >>> k.put_in_pouch('doll') >>> k.put_in_pouch('firetruck') >>> k.put_in_pouch('kitten') >>> k.pouch_contents() ['doll', 'firetruck', 'kitten'] >>> k.jump(1,0) >>> k.jump(1,0) >>> k.jump(1,0) >>> print(k) I am a Kangaroo located at coordinates (3,0)

SOLUTION 3

#A class named Marsupial
class Marsupial:
    #Constructor
    def __init__(self):
        self.lst = []

    #Add to list
    def put_in_pouch(self, item):
        self.lst.append(item)

    #Return List
    def pouch_contents(self):
        return self.lst

#Test
m = Marsupial()
m.put_in_pouch('doll')
m.put_in_pouch('firetruck')
m.put_in_pouch('kitten')
print(m.pouch_contents()) 

3 a,b,c

#Class
class Marsupial:
    #Constructor
    def __init__(self):
        self.lst = []

    #Add to list
    def put_in_pouch(self, item):
        self.lst.append(item)

    #Return List
    def pouch_contents(self):
        return self.lst

#Class
class Kangaroo(Marsupial):
    #Constructor
    def __init__(self,x,y):
        Marsupial.__init__(self)
        self.x = x
        self.y = y

    #Jump
    def jump(self,dx,dy):
        self.x += dx
        self.y += dy

    #Str
    def __str__(self):
        return 'I am a Kangaroo located at coordinates ({},{})'.format(self.x,self.y)

#Test
k = Kangaroo(0,0)
print(k)
k.put_in_pouch('doll')
k.put_in_pouch('firetruck')
k.put_in_pouch('kitten')
print(k.pouch_contents())
k.jump(1,0)
k.jump(1,0)

![image.png](attachment:image.png)

![image.png](attachment:image.png)



QUESTION 4

Write function collatz() that takes a positive integer x as input and prints the Collatz sequence starting at x. A Collatz sequence is obtained by repeatedly applying this rule to the previous number x in the sequence:

x = { 𝑥/2 𝑖𝑓 𝑥 𝑖𝑠 𝑒𝑣𝑒𝑛3𝑥+1 𝑖𝑓 𝑥 𝑖𝑠 𝑜𝑑𝑑

Your function should stop when the sequence gets to number 1. Your implementation must be recursive, without any loops.

>>> collatz(1)

1

>>> collatz(10)

SOLUTION 4

def collatz(x):

    #print value of x
    print(x)
    if x==1:
        return 
    elif x%2==0:
        return collatz(x//2)  #call method recursively
    else:
        return collatz(x*3+1)  #call method recursively

![image.png](attachment:image.png)



QUESTION 5

Write a recursive method binary() that takes a non-negative integer n and prints the binary representation of integer n. >>> binary(0) 0 >>> binary(1) 1 >>> binary(3) 11 >>> binary(9) 1001

SOLUTION 5

def binary(n):
    result = []
    neg = n < 0
    if n == 0:
        return [0]
    elif n < 0:
        n *= -1
    while n > 0:
        result.insert(0, n % 2)
        n //= 2
    if neg:
        result.insert(0, '-')
    return result

![image.png](attachment:image.png)



 QUESTION 6

Implement a class named HeadingParser that can be used to parse an HTML document, and retrieve and print all the headings in the document. You should implement your class as a subclass of HTMLParser, defined in Standard Library module html.parser. When fed a string containing HTML code, your class should print the headings, one per line and in the order in which they appear in the document. Each heading should be indented as follows: an h1 heading should have

indentation 0, and h2 heading should have indentation 1, etc. Test your implementation using w3c.html.

>>> infile = open('w3c.html')

>>> content = infile.read()

>>> infile.close()

>>> hp = HeadingParser()

>>> hp.feed(content)

W3C Mission

Principles

SOLUTION 6

from html.parser import HTMLParser

class DocumentParser(HTMLParser):

    def __init__(self):
        '''Reset the old data in the cache. Initialise the variables.'''
        super().__init__()
        self.reset()
        self.tag_data = []

    def handle_starttag(self, tag, attrs):
        '''Read the start tag'''

        # Check if the tag belongs to heading. If so then append inside the variable to be used later
        if tag in ['h1', 'h2', 'h3', 'h4', 'h5', 'h6']:
            self.tag_data.append({'type': tag, 'data': ''})

    def handle_data(self, data):
        '''Get the data from the tag'''

        # Only for head tag store the data inside the list
        if len(self.tag_data) != 0:
          open_tag_data = self.tag_data.pop()
          if open_tag_data['type'] in ['h1', 'h2', 'h3', 'h4', 'h5', 'h6']:
              open_tag_data['data'] = data
              self.tag_data.append(open_tag_data)

    def print_data(self):
        '''Print the data as per the requirement'''

        # For h1 add no indentation, for h2 add one and so on.
        # print(self.tag_data)
        for data in self.tag_data:
            if data['type'] == 'h1':
                print(data['data'])

            if data['type'] == 'h2':
                print("\t" + data['data'])

            if data['type'] == 'h3':
                print("\t\t" + data['data'])

            if data['type'] == 'h4':
                print("\t\t\t" + data['data'])

            if data['type'] == 'h5':
                print("\t\t\t\t" + data['data'])

            if data['type'] == 'h6':
                print("\t\t\t\t\t" + data['data'])


infile = open('w3c.html')
content = infile.read()
infile.close()
parser = DocumentParser()
content = content.replace("\n", "")
content = content.replace("\t", "")
content = content.replace(" ", "")
parser.feed(content)
parser.print_data()

W3CMission
	Principles



QUESTION 7

Implement recursive function webdir() that takes as input: a URL (as a string) and non-negative integers depth and indent. Your function should visit every web page reachable from the starting URL web page in depth clicks or less, and print each web page's URL. As shown below, indentation, specified by indent, should be used to indicate the depth of a URL. >>> webdir('http://reed.cs.depaul.edu/lperkovic/csc242/test1.html', 2, 0) http://reed.cs.depaul.edu/lperkovic/csc242/test1.html http://reed.cs.depaul.edu/lperkovic/csc242/test2.html http://reed.cs.depaul.edu/lperkovic/csc242/test4.html http://reed.cs.depaul.edu/lperkovic/csc242/test3.html http://reed.cs.depaul.edu/lperkovic/csc242/test4.html

SOLUTION 7

from urllib.parse import urljoin
from html.parser import HTMLParser
from urllib.request import urlopen

class Collector(HTMLParser):

    def __init__(self, url):
        HTMLParser.__init__(self)
        self.url = url
        self.links = []

    
    def handle_starttag(self, tag, attrs):
        if tag == 'a':
            for attr in attrs:
                if attr[0] == 'href':
                    absolute = urljoin(self.url, attr[1])
                    if absolute[:4] == 'http': # collect HTTP URLs
                        self.links.append(absolute)
                        
    def getLinks(self):
        return self.links

def Links(url):
    resource = urlopen(url)
    content = resource.read().decode()
    collector = Collector(url)
    collector.feed(content)
    return collector.getLinks()

def getLinks(self):
        return self.links

global deep
def displayUrl(url,presentDepth):
    padding = len(url) + (presentDepth*indentation)
    string = url.center(padding," ")
    print(string)

def crawl(url,presentDepth):
    

    if(presentDepth>deep): return   
    displayUrl(url,presentDepth)

    links = Links(url)

    for link in links:
        try:
            crawl(link,presentDepth+1)
        except:
            pass

def webdir(url,depth,indent):
    global indentation 
    deep=depth 

    crawl(url, 0)


url = 'http://reed.cs.depaul.edu/lperkovic/test1.html'
webdir(url,2,4)

http://reed.cs.depaul.edu/lperkovic/test1.html
  http://reed.cs.depaul.edu/lperkovic/test2.html  
    http://reed.cs.depaul.edu/lperkovic/test4.html    
  http://reed.cs.depaul.edu/lperkovic/test3.html  
    http://reed.cs.depaul.edu/lperkovic/test4.html 



QUESTION 8

Write SQL queries on the below database table that return:

1, All the temperature data.
2, All the cities, but without repetition.
3, All the records for India.
4, All the Fall records.
5, The city, country, and season for which the average rainfall is between 200 and 400 millimeters.
6, The city and country for which the average Fall temperature is above 20 degrees, in increasing temperature order.
7, The total annual rainfall for Cairo.
8, The total rainfall for each season.


City	Country	Season	Temperature (C)	Rainfall (mm)
Mumbai	India	Winter	24.8	5.9
Mumbai	India	Spring	28.4	16.2
Mumbai	India	Summer	27.9	1549.4
Mumbai	India	Fall	27.6	346.0
London	United Kingdom	Winter	4.2	207.7
London	United Kingdom	Spring	8.3	169.6
London	United Kingdom	Summer	15.7	157.0
London	United Kingdom	Fall	10.4	218.5
Cairo	Egypt	Winter	13.6	16.5
Cairo	Egypt	Spring	20.7	6.5
Cairo	Egypt	Summer	27.7	0.1
Cairo	Egypt	Fall	22.2	4.5

SOLUTION 8

1, SELECT temperature from tablename;
2, SELECT distinct city from tablename;
3, SELECT * from tablename where country='India';
4, SELECT * from tablename where season='Fall';
5, SELECT city, country, season from tablename where rainfaill >= 200
   and rainfall <= 400;
6, SELECT city, country from tablename where temperature>20
   order by temperature ASC;
7, SELECT count(rainfall) from tablename where city='Cairo';
8, SELECT rainfall, count(rainfall) from tablename 
   group by rainfall;



QUESTION 9

 Suppose list words is defined as follows:

>>> words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']

Write list comprehension expressions that use list words and generate the following lists:

(a)  ['THE', 'QUICK', 'BROWN', 'FOX', 'JUMPS', 'OVER', 'THE', 'LAZY', 'DOG']
(b)  ['the', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
(c)  [3, 5, 5, 3, 5, 4, 3, 4, 3] (the list of lengths of words in list words).
(d)  [['THE', 'the', 3], ['QUICK', 'quick', 5], ['BROWN', 'brown', 5], ['FOX', 'fox', 3], ['JUMPS', 'jumps', 5], ['OVER',     
     'over', 4], ['THE', 'the', 3], ['LAZY', 'lazy', 4], ['DOG', 'dog', 3]] (the list containing a list for every word of list 
     words, where each list contains the word in uppercase and lowercase and the length of the word.)
(e)  ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog'] (the list of words in list words containing 4 or 
     more characters.)

SOLUTION 9

(a)  ['THE', 'QUICK', 'BROWN', 'FOX', 'JUMPS', 'OVER', 'THE', 'LAZY', 'DOG']


#(a)
def Upper(words):
    for i in range(len(words)):
        #convert every word in uppercase
        words[i]=words[i].upper()


    return words


words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
#call function
list_Upper=Upper(words)
#print new list
print(list_Upper)
 
===============================================================================================================================

(b)  ['the', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']


#(b)
def Lower(words):
    for i in range(len(words)):
        #convert all words in lowercase
        words[i]=words[i].lower()

    return words


words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
#call method Lower()
list_Lower=Lower(words)
#Print new list
print(list_Lower)

===============================================================================================================================

(c)  [3, 5, 5, 3, 5, 4, 3, 4, 3]

#(C)
def Length(words):
    for i in range(len(words)):
        #convert list having length of each word
        words[i]=len(words[i])

    return words


words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
#call method
list_Length=Length(words)
#print new list
print(list_Length)

==============================================================================================================================

(d)  [['THE', 'the', 3], ['QUICK', 'quick', 5], ['BROWN', 'brown', 5], ['FOX', 'fox', 3], ['JUMPS', 'jumps', 5], ['OVER',   
     'over', 4], ['THE', 'the', 3], ['LAZY', 'lazy', 4], ['DOG', 'dog', 3]]
     
     
     #(d)
def Low_Up_Len(words):
    list=[] #empty list that will store list of upper lower and length of words
    temp=[] #list to create list of each word
    for i in range(len(words)):
        temp.append(words[i].upper())
        temp.append(words[i].lower())
        temp.append(len(words[i]))
        #append temporary list to list
        list.append(temp)

        #initialize temporary list to empty list
        temp=[]


    return list


words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']

#method call
list=Low_Up_Len(words)

#print new list
print(list)

===============================================================================================================================
     
     
(e)  ['quick', 'brown', 'jumps', 'over', 'lazy']   

#(e)
def more_4(words):
    list=[]
    for i in range(len(words)):
        #if word length is 4 or more character
        if len(words[i])>=4:
            
            list.append(words[i])


    return list


words = ['The', 'quick', 'brown', 'fox', 'jumps', 'over', 'the', 'lazy', 'dog']
#call method
list=more_4(words)
#print new list
print(list)










