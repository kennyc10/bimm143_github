# Class 06: R functions


- [Function Basics](#function-basics)
- [3. generate Protein](#3-generate-protein)

## Function Basics

Lets start writting our first silly function to add some numbers:

Every r function has 3 components:

- Name ( we get to pick this)
- Input arguments ( There can loads of these seperated by topic)
- The body ( the R code that does the work)

``` r
add <- function(x, y=100, z=0){
  x + y + z
}
```

I can use this function like any other function as long as R knows it (
i.e Run the code chunk)

``` r
add(1, 100)
```

    [1] 101

``` r
add( x=c(1,2,3,4),y=100)
```

    [1] 101 102 103 104

``` r
add(1)
```

    [1] 101

Functions can have “required” input arguments and “optional” input
arguments. The optional argument are defined with equals default value
(‘y=10’) in the function definition

``` r
add(x=1, y=100, z=10)
```

    [1] 111

> Q. Write a function to return a DNA Sequence of a user specified
> length? Call it ‘generate_dna()’

``` r
generate_dna <- function(size=5){}

students <- c("Jeff", "Jeremy", "Peter")

sample(students, size=5, replace=TRUE)
```

    [1] "Jeremy" "Jeremy" "Jeremy" "Jeff"   "Jeff"  

\##2.generate DNA sequences

Now work with Bases rather than Students

``` r
bases <- c("A", "C", "G", "T")
sample(bases, size=10, replace=TRUE)
```

     [1] "G" "A" "C" "C" "G" "C" "A" "C" "G" "T"

Now I have a working ‘snippet’ of code i can use

``` r
generate_dna <- function(size=5){
  bases <- c("A", "C", "G", "T") 
  sample(bases, size = size, replace=TRUE)
}
```

``` r
generate_dna <- function(size=5, together= TRUE){
  bases <- c("A", "C", "G", "T") 
  sequence <- sample( bases, size = size, replace=TRUE) 
  if(together){
  sequence <- paste(sequence, collapse ="")
  }
  return(sequence)
}
```

``` r
generate_dna(100)
```

    [1] "GGCAATGTTCGTTCGGCACGTTCGAACACTAGAACGGAGGAGTAAGCTACGGACCGCAGGGTATGGAACGGTCACTTGAAAGGACTCTGACCGCAGTTTG"

## 3. generate Protein

> Q. Write a protein sequence generating function that will return
> sequences of a user specified length?

> Q. Generate random protein sequence

We can get the set of 20 natural amino acids from the **bio3d** package

``` r
aa <- bio3d::aa.table$aa1[1:20]
aa
```

     [1] "A" "R" "N" "D" "C" "Q" "E" "G" "H" "I" "L" "K" "M" "F" "P" "S" "T" "W" "Y"
    [20] "V"

``` r
generate_protein <- function(size=5, together=TRUE){
  aa <- bio3d::aa.table$aa1[1:20]
  sequence <- sample( aa, size = size, replace=TRUE)
  if(together){
  sequence <- paste(sequence, collapse ="")
  }
  return(sequence)
}
```

``` r
generate_protein(4)
```

    [1] "GICE"

We can fi this inabiliuty to genertae multiple sequences by either
editing and adding to the function body code (e.g. A for loop\_ or. by
using the R \*\* apply\*\* family of utility functions.

``` r
sapply(6:12, generate_protein)
```

    [1] "YASNGW"       "VANTYWC"      "EKVNTYIP"     "VVWCYVGQC"    "NKKDYNNKYF"  
    [6] "GVYMTKGWAHE"  "VGCPCKIAGAIY"

``` r
generate_protein(7)
```

    [1] "DYCFSCR"

``` r
generate_protein(8)
```

    [1] "MILCPWIF"

``` r
generate_protein(9)
```

    [1] "KSCNWNAYP"

it would be cool and useful if i could get FASTA format output

``` r
ans <- sapply(6:12, generate_protein)
ans
```

    [1] "RVMSIF"       "NFYTANR"      "LEFPPTKK"     "KEEQVGGGS"    "MESHWSVDAK"  
    [6] "CKNPEPSSFAH"  "VVVSQSMVWYDK"

``` r
cat(ans, sep="\n")
```

    RVMSIF
    NFYTANR
    LEFPPTKK
    KEEQVGGGS
    MESHWSVDAK
    CKNPEPSSFAH
    VVVSQSMVWYDK

I want it to look like

> ID.6

the function ‘paste()’ and ‘cat()’ can help us here…

``` r
cat(paste(">ID.", 6:12, "\n", ans, sep=""), sep="\n")
```

    >ID.6
    RVMSIF
    >ID.7
    NFYTANR
    >ID.8
    LEFPPTKK
    >ID.9
    KEEQVGGGS
    >ID.10
    MESHWSVDAK
    >ID.11
    CKNPEPSSFAH
    >ID.12
    VVVSQSMVWYDK

``` r
id.line <- paste (".ID", 7:12, sep="" )
id.line
```

    [1] ".ID7"  ".ID8"  ".ID9"  ".ID10" ".ID11" ".ID12"

``` r
id.line <- paste (".ID", 6:12, sep="" )
seq.line <- paste(id.line, ans, sep="\n")
cat(seq.line, sep="\n", file="myseq.fa")
```

``` r
seq.line <- paste(id.line, ans, sep="\n")
cat(seq.line, sep="\n", file="myseq.fa")
```

> Q.determine if these sequences are found in nature

I BLASTp searched my FASTA format sequences against NR and found that
length 6,7, 8 are not unique and can be found in the database with 100%
coverage and 100% identity.

Sequences 9-12 are unique and cant be founf in the databases
