
<h1><b><center>Chmod</center></b></h1>

In UNIX based systems, there are 3 types of owners (U or G or O) of a file (<a href="https://en.wikipedia.org/wiki/Everything_is_a_file">Everything in Linux is a file!</a>)


<b>User (U)</b> - The user is also the owner of the file. The creator of the files becomes the owner of the file.


<b>Group (G)</b> - A group can contain multiple users. All the users in the group will have the same type of permissions or access.


<b>Other (O)</b> - All the other users who have access to the file.  


So, when ever we see chmod we are always seeing this format of results, mainly:

fUUUGGGOOO or dUUUGGGOOO 

total of 10 bits. Can be represented as: - - - - - - - - - -


 <b><font color="white">Permissions:</font></b>

We talked about the owners of the file above. Different types of owners (U, G, or O) have different types of permissions/access (R or W or X):

<b>Read (R)</b>: read permission gives you the ability to open and read a file. The read permission on a directory means that we have access to list the directory.

<b>Write (W)</b>: write permission gives you the authority of modifying the contents of the file. Write permission on a directory gives you the permission to add, delete or rename files in the directory. 

<b>Execute (X)</b>

 In Unix based systems, you cannot run a file unless the execute (X) permissoin is set. If the X is not set, you might still be able to view the program code(provided read & write permissions are set), but not run it. (just like .exe executable in Windows!)

For example, lets understand what the following modes mean and how they are calculated:
