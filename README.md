# pytLoc
pytLoc is a python tool that locks python source files using a one time pad lock. It helps to securely storing and sharing python source files. <br/>
         **Author**: [Gilda Bansimba](https://github.com/GildaRech/GildaRech)<br/>
         **usage**: **`from pytLoc import pytLoc`**<br/>
         **Python Package Index**: [Download / view on pypi](https://pypi.org/project/pytLoc/) <br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **`pytLoc.pytLoc(*args).[method]`** <br/>
         Options and methods. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This class represents the heart of pytLoc.<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It takes optionnal arguments:<br/>
       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; -either a list of file names in the current working directory. E.g: ***`pytLoc.pytLoc("file1.py")`***<br/>
       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;or ***`pytLoc.pytLoc("file1.py", "file2.py")`***<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-either "." to obfuscate all python files in the current working directory. E.g: ***`pytLoc.pytLoc(".").loc(key)`***<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-either "*" to obfuscate all python files in the current working directory and in its subfolders. E.g: ***`pytLoc.pytLoc("*").loc(key)`***<br/>
       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; -either "`***`" to obfuscate all python source code files stored in the entire disk. E.g: ***`pytLoc.pytLoc("***").loc(key)`***<br/>
       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ***key*** --> the key is a string: a phrase or key string or a list of words or strings. E.g: key="hello"; key="hello, h*cb45#".<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ***genKey(key, leng)*** --> generates a one time pad of length "leng" key from a the key "key".<br/>
               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; This key is generated randomly using the secure hash algorithm with 512 bits. To do so, <br/>
               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; it uses the composition function of functions initialized at sha512(key) concatenated with <br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the footprints of consecutive concatenation of footprints up to the length "leng".<br/>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;***loc(key)*** --> locks / obfuscates python files indicated in pytLoc with the one time pad key generated from
                the key "Key"<br/>
        ***`unloc(key)`***       --> unlocks / de-obfuscates python files indicated in pytLoc with the one time pad key generated
                             from the key "Key".<br/>
        ***`genKey(key, len)`*** --> generates a one time pad security key of length len derived from key.<br/>
        ***`sig(file)`***        --> computes a hash of file.<br/>
        ***`check(file)`***      --> function that checks the integrity of a locked python source.<br/>
        E.g: 1- *OBFUSCATE / LOCK A PYTHON FILE or PYTHON FILES IN THE CURRENT WORKING DIRECTORY*<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to obfuscatE the file "file1.py" located in the current working directory with the one time pad generated from key "hello",<br/>
               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; --> ***`pytLoc.pytLoc("file1.py").loc("hello")`*** which generates the file "LOCKED_file1.py" in the same directory. This file is obfuscated.<br/>
               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; to DE-obfuscatE the file "LOCKED_file1.py" located in the current working directory with the one time pad generated from key "hello",<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc("LOCKED_file1.py").unlock("hello")`*** which generates back the file "UNLOCKED_file1.py" which is equal to "file1.py" in the same 
                    directory.<br/>
             2- *OBFUSCATE / LOCK ALL PYTHON FILES LOCATED IN THE CURRENT WORKING DIRECTORY*<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to obfuscatE all python files located in the current working directory with the one time pad generated from the key "hello",<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc(".").loc("hello")`*** which generates the files "LOCKED_....py" in the same directory. These files are obfuscated.<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to DE-OBFUSCATE / UNLOCK all the obfuscated python files "LOCKED_....py" located in the current working directory with the one time pad generated from
                the key "hello", <br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc(".").unlock("hello")`*** which generates back the files "UNLOCKED_....py" in the same directory.<br/>
             3- *OBFUSCATE / LOCK ALL PYTHON FILES LOCATED IN THE CURRENT WORKING DIRECTORY AND ITS SUB-DIRECTORIES*<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to obfuscatE all python files located in the current working directory and its sub-directories with the one time pad generated from the key "hello",<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc("*").loc("hello")`*** which generates the files "LOCKED_....py" in current working directory and all its corresponding sub-directories.<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to OBFUSCATE / LOCK all python files located in the current working directory and its sub-directories, <br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc("*").unlock("hello")`*** which generates the files "UNLOCKED....py" in the current working directory and all its corresponding sub-directories.<br/>
             4- *OBFUSCATE / LOCK ALL PYTHON FILES LOCATED IN THE ENTIRE DRIVE PARTITION*<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to obfuscatE all python files located in the entire drive partition with the one time pad generated from the key "hello",<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc("***").loc("hello")`*** which generates the files "LOCKED_....py" in wherever directory or sub-directory where python files are found.<br/>
                &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to DE-obfuscatE all python files located in the entire drive partition with the one time pad generated from the key "hello",<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--> ***`pytLoc.pytLoc("***").unlock("hello)`*** which generates the files "UNLOCKED....py" in wherever directory or sub-directory where locked python files are found.<br/>

     NOTE: when calling pytLoc without parameter `delete` or with parameter `delete=False`, (E.g `pytLoc.pytLoc("file1.py").loc(key)` or <br/>
     `pytLoc.pytLoc("file1.py", delete=False).loc(key)` ), the original files are not deleted. and with parameter `delete=True`, original files are deleted <br/>
