# AutoTest - CI for Tamarin Prover



AutoTest is a script that runs tests for Tamarin either locally or on [Travis](https://travis-ci.com/github/tamarin-prover/tamarin-prover). 



## Usage



Basic usage is to execute the script without any arguments. To do so, go to the directory root :

```bash
$ cd tamarin-prover
```

and type :

```bash
$ python3 autoTest.py
```

This command will first `make` the tests `case-studies` and then compare the results with the reference directory `case-studies-regression`. 

(Warning : make command can take more than an hour to run)



## Arguments

Here is a list of the arguments and how to use them properly.

#### -f or --fast

This argument is used to run tests in fast mode (around 10 minutes instead of an hour)



 