# property-manager
manage and refine properties files in SpringBoot or any java application

## property-refiner
As we continue to develop applications, we tend to add properties to application.properties files. The addition of new properties at random lines numbers with/without comment lines, makes the file less readable.
The idea of this feature is to improve the readability of the contents.

One of the solution is to create PropRefiner tool which reads the contents, sets proper order and write the refined contents back to the file.
Suppose we have an application.property with below content:

<pre>
#comment-B
key3=value3
key2=value2
#comment-A
key1=value1
</pre>

Upon running the PropRefiner, the content should look like:

<pre>
#comment-A
key1=value1
#comment-B
key2=value2
key3=value3
</pre>

### solution
*   create Map of Map.
*   read contents of application.properties file line by line.
*   collect all consecutive comment lines as key for the outer Map.
*   the value for the outer map will be Map of key-value pairs of the following key=value formatted lines.
*   below is what it looks like after whole file is read:
<pre>
#comment-B => {key3=value3
               key2=value2
               }
#comment-A => {key1=value1
              }
</pre>
*   now go ahead and sort each of the inner Map entries e.g. key=value
*   get the key from the first entries of each of these inner Maps. e.g. key2, key1.
*   add these keys along with the outer map's key in a new Map e.g. key2 => #comment-B, key1 => #comment-A
*   sort this new Map
*   go through the entries of this new Map and dump entries from the first Map by reading the value of the new Map
e.g. dump all sorted inner map entries for key '#comment-A' and then for key '#comment-B'.


#Note:
everyone is welcome to contribute to this and propose solution.
Encourage you to contribute a working script (preferably in Python).

Thank you.
