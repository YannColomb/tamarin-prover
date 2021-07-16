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

It uses the `case-studies/fast-tests` directory and compare it to the `case-studies-regression/fast-tests` directory.

This argument need to be used in Travis or else the build won't pass due to either a lack of memory error (137) or a "no output received in the last 10m" error. 



#### -ed or --except-dir

This argument is used to remove directories (or files) from the comparison test. 

This argument **should** be used in every script to remove at least the file `system.info`.

The syntax is the following : `--except-dir=system.info,sapic,dh` to remove the file `system.info` and the directories `sapic` and `dh`.



#### -notime or --without-times

This argument allows the script not to compute processing times.

It is useful for Travis on which processing times don't matter.



#### -nofn or --without-filename

This argument runs the script without adding filenames into files and output. 

It is useful for Travis to buy time on the build.



#### -grad or --time-graduation

This argument colorize processing times using 2 values. Default values are 0.3 and 0.8.

It compares the old time with the new one and colorize them from green to red depending on whether the new time is 30% (0.3 for the first value) higher or lower than the old one (green), or between 30% and 80% (0.8 for the second value) (orange), or higher or lower than 80% (red).

The syntax is the following : `-grad=0.3,0.8`



#### -nom or --no-make

By default the script runs a make command, if you don't need it because you've already done it, use this argument.



#### -showt or --show-all-times

This argument will run script showing you all processing times without colors nor condition.



#### -t or --time-gap

This argument allows you to show the processing times that respect a condition.

The  syntax is the following : `-t 0.5` will show you new times that are 50% lower than the old ones. 



#### -node or --no-display-errors

This argument runs script without displaying errors.

This argument can be combined with `-nodf` to only have errors in a file and not in the user output.



#### -nodf or --no-delete-final-files

This argument will keep the file of time results and also the one with errors if there is some.



#### -lel or --limit-error-line

This argument allows two lines to be considered the same if they have X% resemblance.

For instance, default value is 1 so two lines are the same if they have 100% resemblance (so they are the same).

This is used to compare lines from `case-studies` and `case-studies-regression` after a `diff` command.

The syntax is the following : `-lel 0.8`



#### -nodur or --no-display-duration

This argument will show you the duration of the script at the end of it.



####  -dup or --allow-duplicate

The `make` command creates files `*.spthy` with processing times in them and a summary of it. These times are often the same as the summaries, so duplicated lines are by default deleted. You can however allow them with this argument.



#### -ask or --ask-for-deletions

This argument runs the script so that you will be asked whether you want to delete some files that can be a problem for the script.

By default these kind of files are deleted without asking.



#### -wkeep or --with-git-keep

This argument recreates empty directories in `case-studies` with `.gitkeep` in them.

This is not a useful command. It is only useful if you want to remove the `mkdir` command from `.travis.yml` and if you want to push all directories on git. (Not recommended)



#### -d or --debug

Use this argument to run the script in debug mode. This won't delete useful temporary files.

 

## Adding new files to test

To add new files to test, you have to put a reference file in the `case-studies-regression` directory. This reference file **must** **be** an output of a make command.

If you want to add it in fast-tests (and so in Travis), you need to add a Target in the Makefile after `fast-case-studies` and to add the reference file in the `case-studies-regression/fast-tests` subdirectory.