# A simple example

This directory contains a simple "Hello world" hole file & an example Ruby implementation. You can use it to learn how everything works, or as a way to help people get started and make sure their setup works. 

To recap, you should pass Golfcaddy a hole file and a command to run your program. Golfcaddy presumes the last argument is the source code for your program (it uses this to score your implementation).


## Running from the repo

If you've checked out a copy of the Golfcaddy repo, you can run the example from the repository root: 

```bash
user@host golfcaddy$ ./golfcaddy example/helloworld.yaml ruby example/helloworld.rb
```


## Running as a code golf player

Things look a little neater when you're a player, as you'll have Golfcaddy in the same directory as your hole file & implementation:

```bash
user@host golfcaddy$ ./golfcaddy helloworld.yaml ruby helloworld.rb
```


## Expected output

```plaintext
YOUR MISSION: No matter what the input, output the string "Hello, world!". This is a good way to test your overall setup.


....
Success! 4 tests passed.
Your code has a score of 18 (lower is better).
```
