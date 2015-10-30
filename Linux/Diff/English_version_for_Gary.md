# `diff` tutorial (Motivated by Gary)

#### Written by: Henry Tseng

Instead of doing a manual comparasion between the sample output and your program's
output, you can use a great tool called `diff` to help you.

Before we start, let's learn to save the output into a file first.

### Method one: redirection

It's just like manually entering the input into your program, so no code changes
needed.

After compiling your program, and let's assume the executable file is named `a.out`,
input file named `input.txt`, and output file with your desired name, `output.txt` to be
concise. Simple run:
```
./a.out < input.txt > output.txt
```
to load the data in `input.txt` to the program and store the output into `output.txt`.

If you just want to load the data from `input.txt` and show the output on the screen, you can run:
```
./a.out < input.txt
```

### Method two: `freopen()`

Simply add two lines of code to the start of the `main()` function and you are good to go!

The syntax of `freopen()` is very simple:
```
freopen("file name", "r/w", stdin/stdout);
```

For example，if the input data is in `input.txt`, and the desired output file name is `output.txt`,
simply add these two lines of code to the start of the `main()` function:
```
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
```

To check if `freopen()` successfully creates/reads the file or not, check the return
value. If it's NULL, then something went wrong.
```
if(freopen("file name", "r/w", stdin/stdout) == NULL)
    YOUR_ERROR_MESSAGE_HERE;
```

# Usage of `diff`

Assume that your answer to be compared against is in `answer.txt`, then simply run
```
diff answer.txt output.txt
```
to compare `output.txt` with `answer.txt`.

If no message showed up after running the command, then your code has passed the test!
Otherwise, it's time to debug. :(
