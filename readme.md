# Golfcaddy

Golfcaddy is a program to help you run code golf sessions. It's a simple, language-agnostic way of ensuring that everyone's code works correctly & is scored fairly. 

Golfcaddy's only requirement is Ruby, which comes as standard with macOS and Linux. Players should be able to run programs from the commandline, and be able to write simple programs. Golfcaddy works best if you can send files to all your players simultaneously (eg. via Slack). 

## What is code golf?

Code golf is a programming exercise where the goal is to write a program in the **shortest way possible**. The normal qualities we look for in our programs - clarity, maintainability, extendability, and so on - have **absolutely no place** in code golf. Cleverness, concision, and shortcuts are all encouraged. 

Code golf's a fun & educational exercise that encourages players to think about their code in a new way. It works well as a pair programming exercise - players work together not just to write the program, but to optimise it for character count.


## Using Golfcaddy

1. **Send your participants a copy of `golfcaddy`**. They should: 
    1. Create a new directory, & place Golfcaddy in it:
        ```bash
        mkdir codegolf
        mv ~/Downloads/golfcaddy codegolf
        cd codegolf
        ```
    2. Ensure they can run Golfcaddy:
        ```bash
        ./golfcaddy
        ```

        If it's working, they should see:
        ```plaintext
        Your golfcaddy is ready to play! 

        Usage: golfcaddy <holefile> <runner> <source_file>
        eg. golfcaddy hole1.yaml ruby stringcounter.rb
        ```
2. **Send your players a hole file**. These describe the challenge and act like unit tests for the player's program. There [are a number to choose from](holes/), of varying difficulty and duration. The players should put this in the same directory as Golfcaddy.
    ```bash
    mv ~/Downloads/fizzbuzz.yaml codegolf
    ```
3. **Create an empty program, and tell Golfcaddy to run it**. Golfcaddy doesn't care what language you use, but I'm going to use Ruby. The first argument passed to Golfcaddy is the hole file; the rest of the arguments are presumed to be how to run the program. The last one is treated as the source code for your program.
   ```bash
   touch fizzbuzz.rb
   golfcaddy fizzbuzz.yaml ruby fizzbuzz.rb
   ```
   Your program doesn't do anything yet, so Golfcaddy will describe the challenge and tell you what it tried: 
   ```plaintext
   YOUR MISSION: Given a number, output all the numbers from 1 to that number as a comma-separated list. But! If a number is a multiple of three, it should output "fizz" instead. If it's a multiple of five, it should output "buzz" instead. If it's a multiple of both, then it should output "fizzbuzz".


   F
   Failed!

   Given an input of '1', I expected the output to be:
   1

   But, your program produced no output on stdout. :(
   ```
4. If your program half works, Golfcaddy will tell you what went wrong. Let's create a simple Ruby program that prints numbers from 1 to _n_ as a comma-separated list:
   ```bash
   echo "puts (1..gets.chomp.to_i).to_a.join(', ')" > fizzbuzz.rb
   golfcaddy fizzbuzz.yaml ruby fizzbuzz.rb
   ```
   This program works fine for "1", and "2", but it's not going to output "Fizz" instead of "3": 
   ```plaintext
   YOUR MISSION: Given a number, output all the numbers from 1 to that number as a comma-separated list. But! If a number is a multiple of three, it should output "fizz" instead. If it's a multiple of five, it should output "buzz" instead. If it's a multiple of both, then it should output "fizzbuzz".


    .F
    Failed!

    Given an input of '5', I expected the output to be:
    1, 2, fizz, 4, buzz

    But, your program produced:
    1, 2, 3, 4, 5
    ```
5. **When players produce a working program then Golfcaddy prints their score**. Golfcaddy doesn't care about whitespace or newlines, so you can space things out to keep a little readability in your program.
    ```plaintext
    YOUR MISSION: Given a number, output all the numbers from 1 to that number as a comma-separated list. But! If a number is a multiple of three, it should output "fizz" instead. If it's a multiple of five, it should output "buzz" instead. If it's a multiple of both, then it should output "fizzbuzz".


    .......
    Success! 7 tests passed.
    Your code has a score of 154 (lower is better).
    ```


## Tips for running a fun code golf session

* Allow at least an hour to run the session, ideally two. That's enough time to demo Golfcaddy, get people set up, run 3-6 holes, and share solutions at the end.
* Don't send players a link to this repository. It's fairer if nobody's examined the problems ahead of time.
* Space out your holes in 10-15 minute intervals, based on how players are getting on. Allow players to go back and improve their scores on older holes, if they like, but your goal should be for everyone to finish all holes. 
* Code golf works best when players are in teams of 2 or 3. As well as sharing ideas, it helps players not get completely stuck.
* Keeping a leaderboard of teams & their best score for each hole on a whiteboard is a _great_ way of encouraging friendly competition & letting people know there's a shorter way of doing things. 
* You can use compiled languages with Golfcaddy too, as long as your program doesn't care about its command line arguments. Just put your source file name as the last argument in your golfcaddy command. For instance, if you'd written a `fizzbuzzingo` program in Go: 
    ```bash
    ./golfcaddy fizzbuzz.yaml fizzbuzzingo fizzbuzz.go
    ```
    Golfcaddy won't ensure that your source file got compiled, though - that's down to your players.
* While Golfcaddy is language-agnostic, I **strongly recommend** not using JavaScript unless everyone's using JavaScript. Working with `stdin` and `stdout` is hard to explain in JavaScript, and very verbose. But if you do attempt it, here's an example ES6 program that replaces the word "cat" with "dog":
    ```javascript
    process.stdin.pipe(require('stream').Transform({
      transform: (buffer, encoding, callback) => {
        callback(null, buffer.toString().replace("cat", "dog"));
      }
    })).pipe(process.stdout);
    ```

## License

Golfcaddy is released under the GPL.


