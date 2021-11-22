CREATING QUEUES AND PRINTING COMMENTS IN LOG FILE 
=================================================

This file describes the approach of adding comments in CUPS files and printing 
them in default log files.


ADDING PRINTERS & CREATING PRINT QUEUES 
---------------------------------------

I created printer using lpadmin command. 

    /usr/sbin/lpadmin -p testing1 -E -v file:/dev/null
    

Next to create print jobs I used the lp command.

    lp -d testing1 <file_name -> here I gave an image >

Kindly note that for installation I have used the default configuration and each and 
every command is executed in the home directory. The location of these commands may 
vary according to the configuration used at the time of installation. 


FINDING LOG FILES AND RELEVANT CODE
-----------------------------------

I found the default location of log files in cups/conf/cups-files.conf.in. The log files 
were stored in /var/log/cups. There were two log files, access_log and error_log. I noted
some of the keywords in access_log and used grep command to find relevant files that could
generate them.

    grep -r "localhost - -" cups/

The result displayed many files. The most relevant file found was log.c located in scheduler
folder. I went through the file and found a function cupsFilePrintf().

The function accepted two arguments, i.e. the file name and the text to be written in that
file.


ADDING COMMENTS AND PRINTING THEM
---------------------------------

I added some comments in the cupsFilePrintf() function of access_log. I added "This comment was added by Deepak Khatri" in the function. 
After changing the file. Enter make and make install commands again. 
  ```
  make clean
  make
  sudo make install
  ```

Again give any print job and check the log files. The added comments will be printed in 
the log files.
