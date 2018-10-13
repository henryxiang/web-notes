## How to Make Perl Regex One-Liners

Perl-one liners are powertools that get a lot of work done with a single command. You can use them on the Unix command-line—or indeed on the command line of any OS where Perl is installed.

### Input File
All our one-liners assume we are working with a file called input_file containing these lines:
```
cat bat carrot
book true blue
red caramel
```

### Regex
All our one-liners assume we are working with this regex: `\bc\w+`. The idea is to match words that start with the letter c. In our input, these words are cat, carrot and caramel. 

### General Notes on Syntax

* The `-e` (execute) flag is what allows us to specify the Perl code we want to run right on the command line. The Perl code is within quotes.
* The `-n` flag feeds the input to Perl line by line.
* `-0777` changes the line separator to undef, letting us to slurp the file, feeding all the lines to Perl in one go.
* All the examples assume we're working on one file called input_file, but you could specify multiple files with input_file input_file2 input_file3 or with *.txt 
* All the examples assume we're working on one file called input_file, but you could instead pipe some output to the one-liner, e.g. `echo $PATH | perl…` 
* The `-p` flag (printing loop) processes the file line by line and prints the output.
* To replace directly in the file you can use the `-i` flag… but first test your one-liner without the -i to make sure it's what you want.
* If you're planning to use (*SKIP)(*F), remember this only works in Perl 5.10 and above: check your Perl version with `perl -v`
* The perl command is in apostrophes, and escaping those is hard work… So if your regex happens to contain apostrophes, first place it in an env variable then refer to it by name, e.g. `env mypattern="'\w+" perl -0777 -ne 'while(m/$ENV{mypattern}/g){print "$&\n";}' input_file` 

### Tasks for Perl Regex One-Liners

Task 1: Process the file line by line, and return all matches. We expect to match cat, carrot, caramel.
```bash
perl -ne 'while(/\bc\w+/g){print "$&\n";}' input_file
```

Task 2: Process the file line by line, and return all matching lines. We expect to match lines 1 and 3.
```bash
perl -ne 'print if /\bc\w+/' input_file
```

Task 3: Process the file line by line, and return the first match of each line. We expect to match cat and caramel.
```bash
perl -ne 'print "$&\n" if /\bc\w+/' input_file
```

Task 4: Process the file as a block, and return all matches. We expect to match cat, carrot, caramel.
```bash
perl -0777 -ne 'while(m/\bc\w+/g){print "$&\n";}' input_file
```

Task 5: Process the file as a block, and return the first match. We expect to match cat.
```bash
perl -0777 -ne 'print "$&\n" if /\bc\w+/' input_file
```

Task 6: Process the file as a block, and replace all matches with ZAP.
```bash
perl -0777 -pe 's/\bc\w+/ZAP/g' input_file
```

Task 7: Process the file as a block, and replace the first match with ZAP.
```bash
perl -0777 -pe 's/\bc\w+/ZAP/' input_file
```

Task 8: Process the file line by line, and replace all matches with ZAP.
```bash
perl -pe 's/\bc\w+/ZAP/g' input_file
```

Task 9: Process the file line by line, and replace the first match with ZAP.
```bash
perl -pe 's/\bc\w+/ZAP/' input_file
```

Task 10: Process the file as a block, and split.
```bash
perl -0777 -ne 'if(@r=split(m/\bc\w+/,$_)){foreach(@r){print "$_\n";}}' input_file
```

Task 11: Process the file line by line, and split.
```bash
perl -ne 'if(@r=split(m/\bc\w+/,$_)){foreach(@r){print "$_\n";}}' input_file
```

### References
[Perl Regex One-Liners](http://www.rexegg.com/regex-perl-one-liners.html)