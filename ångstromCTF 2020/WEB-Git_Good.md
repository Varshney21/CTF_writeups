## WEB Git Good

As the name suggest there would be some think related to GitHub. Response of request to `/.git/logs/HEAD` with status code 200.

Use gitdumper to download all available files in the .git folder form the server https://github.com/internetwache/GitTools/tree/master/Dumper

To check all the commits made:
![gitdumper](https://i.imgur.com/82XQRbd.png)

There are two commits done in the local repository on the server:
![commit](https://i.imgur.com/VXdfHZo.png)

find the tree object hash for the initial commit by using `git cat-file` which provide content or type and size information for repository objects.:
![com1](https://i.imgur.com/gGe1ycm.png)

check for all the contents of the initial commit by uding `git cat-file -p` to pretty-print the contents of <object> based on its type.
![cat-file](https://i.imgur.com/F396BQF.png)

You can find the object hash for file `thisistheflag.txt` 

From the browser request to /.git/objects/0f/52598006f9cdb21db2f4c8d44d70535630289b to download thisistheflag.txt. The first two bytes of the hash is the dirname in Objects dir.

Use python zlib module to decompress the data and print the contents. And you will find the flag.
![flag](https://i.imgur.com/Nog9579.png)
