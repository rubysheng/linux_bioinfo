# How to create a shell script

## General process of creating your own scripts

1. understand your project: **aim**, **Input** and desired **Output**
2. draw a flowchart to help you clarify the process
3. divide it with several steps
4. realize each step with your code


## For this project
### 1 Aim
Run programs several times with different input

#### ? How to complete the task manually
##### Recall

We used two programs - `water` and `needle`. There are several ways to run these programs.

1. No parameter:

    ```
    $ needle
    Needleman-Wunsch global alignment of two sequences
    Input sequence: sequences.fasta:sequence1
    Second sequence(s): cloning_vector.fasta     
    Gap opening penalty [10.0]:
    Gap extension penalty [0.5]:
    Output alignment [sequence1.needle]: seq1-cv.needle.out1
    ```

2. Had two input files in the command line:

    ```
    $ needle sequences.fasta:sequence1 cloning_vector.fasta
    Needleman-Wunsch global alignment of two sequences
    Gap opening penalty [10.0]:
    Gap extension penalty [0.5]:
    Output alignment [sequence1.needle]: seq1-cv.needle.out2
    ```

3. What if we want to keep only the command line:

  check the manual first: `needle -h`

![needle](/Users/ruby/Desktop/needle_h.png)

Here, qualifiers are the parameters in running this program.
*Mandatory* qualifiers are the must. *optional* are not necessary.

So the if we only use one command line with full names of *Mandatory* qualifiers. It should be look like this:

```
$ needle -asequence sequences.fasta:sequence1 -bsequence cloning_vector.fasta\
         -gapopen 10 -gapextend 0.5 -outfile seq1-cv.needle.out3
Needleman-Wunsch global alignment of two sequences
```

Or, wehn we just use default gap penalties (`-gapopen 10 -gapextend 0.5`), we can use a optional parameter `-auto`(Turn off prompts).

```
$ needle sequences.fasta:sequence1 cloning_vector.fasta \
         -outfile seq1-cv.needle.out4 -auto
```

##### Command lines

In the folder "**lab7**" (containing `sequences.fasta` and `cloning_vector.fasta`):

```
$ needle sequences.fasta:sequence1 cloning_vector.fasta -outfile seq1-cv.needle.out -auto
$ needle sequences.fasta:sequence2 cloning_vector.fasta -outfile seq2-cv.needle.out -auto
$ needle sequences.fasta:sequence3 cloning_vector.fasta -outfile seq3-cv.needle.out -auto
$ water sequences.fasta:sequence1 cloning_vector.fasta -outfile seq1-cv.water.out -auto
$ water sequences.fasta:sequence2 cloning_vector.fasta -outfile seq2-cv.water.out -auto
$ water sequences.fasta:sequence3 cloning_vector.fasta -outfile seq3-cv.water.out -auto
```

***? What is the pattern of these command lines?***

![cmd-pattern](/Users/ruby/Desktop/pattern.png)

### 2 Flowchart
![process](/Users/ruby/Desktop/process_dr.png)

### 3 Steps

+ create some variables for each highlighted region
  - yellow : don't need because we will run two programs
  - red - `N` : will change from 1 to 3, one by one
    - change with a loop : `for` or `while`
  - green : don't need because we will run two programs

+ create some variables for different parameters in these command lines
  - `ASEQUENCE`
  - `BSEQUENCE`
  - `OUTFILE`

  ***？How to define a variable***  
  `variable_name=variable_value`. For example:
  ```
  NAME="Zara Ali"
  ```  

+ main body of the script
  - `needle`
  - `water`

  ***？How to use a defined variable***  
  To access the value stored in a variable, prefix its name with the dollar sign ($):
  ```
  echo $NAME
  ```

+ use a loop to run programs several times
  - change `ASEQUENCE` with `N`
  - change `OUTFILE` with `N`

  ***？How to use a loop***  
  ```
  for VARIABLE in 1 2 3 4 5 .. N
  do
    command1
    command2
    commandN
  done
  ```
