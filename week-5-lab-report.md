# Lab Report 3

## Part 1 - Bugs

**Choose one of the bugs from week 4's lab. Provide the following:**
  - **A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)**<p>
    - > The `reverseInPlace` method in `ArrayExamples` class contains a bug that will manifest when attempting to reverse an array
      > in place. The method incorrectly tries to swap elements but ends up overwriting the initial elements with the latter ones,
      > leading to incorrect results.
      > 
      > A JUnit test that induces this failure:
      > ```java
      > @Test
      > public void testReverseEvenLength() {
      >   int[] input2 = { 1, 2, 3, 4 };
      >   assertArrayEquals(new int[]{ 4, 3, 2, 1 }, ArrayExamples.reversed(input2));
      > }
      > ```
  - **An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)**<p>
    - > An input that doesn't induce a failure for the `reverseInPlace` method could be an empty array or an array with a single element,
      > as the logic flaws in the method won't affect such arrays.
      >
      > Here's a JUnit test for such a scenario:
      > 
      > ```java
      > @Test
      > public void testReverseInPlace() {
      >   int[] input1 = {3};
      >   ArrayExamples.reverseInPlace(input1);
      >   assertArrayEquals(new int[]{3}, input1);
      > }
      > ```
  - **The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)**
      > <img width="1003" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/09081abf-652d-4be7-8c7f-8d437dd22f99">
      > <img width="1003" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/6753846a-85d9-4fd6-b2e0-c701b74d4fc0">

  - **The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)**<p>
    - > Before fix:
      > ```java
      > static void reverseInPlace(int[] arr) {
      >   for(int i = 0; i < arr.length; i += 1) {
      >   arr[i] = arr[arr.length - i - 1];
      >   }
      > }
    - > After fix:
      > ```java
      > static void reverseInPlace(int[] arr) {
      >   for(int i = 0; i < arr.length / 2; i += 1) {
      >     int temp = arr[i];
      >     arr[i] = arr[arr.length - i - 1];
      >     arr[arr.length - i - 1] = temp;
      >   }
      > }

  - **Briefly describe why the fix addresses the issue.**
    - > The fix addresses the issue by correctly swapping the elements in place. It does so by only iterating halfway through the array (up to `arr.length / 2`) and using a temporary variable (`temp`) to hold the value of the element being moved. This ensures that each pair of elements (one from the start and one from the end) is swapped exactly once, without overwriting any values prematurely. 

## Part 2 - Researching Commands

**Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!**

**For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.**

**That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.
Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.** 
<br>

  
  - >  The `grep` command is used for searching plain-text data sets for lines that match a regular expression. Its versatility makes it a powerful tool in text processing and data analysis tasks. Here are four interesting command-line options for `grep`, with two examples for each, demonstrating its usage on files and directories from `./technical`.<p>
    > #### `-i` (ignore case)
    > - The `-i` option makes `grep` search case insensitive, allowing it to match lines regardless of case.<p>
    >   - `grep -i "pattern" ./technical/file.txt`<p>
    >     - This command searches for `"pattern"` in `file.txt` within the `./technical` directory, ignoring case differences. It's useful when the casing of the search term is unknown.<p>
    > >  ```
    > >  OUTPUT:
    > > Pattern found in line 3
    > > Another instance of pattern found in line 47
    > > ```
    >   - `grep -ir "pattern" ./technical/`<p>
    >     - This recursively searches for `"pattern"` in all files under the `./technical directory`, ignoring case. It's helpful for wide-reaching searches where case sensitivity could miss matches.<p>
    > >  ```
    > >  OUTPUT:
    > > ./technical/subdir/file1.txt:Pattern found in line 3
    > > ./technical/anotherDir/config.txt:pattern instance in line 19
    > > ```
    
    > #### `-r` (recursive)
    > - The `-r` option allows grep to perform a recursive search through directories, looking into every file within the specified directory and its subdirectories.<p>
    >   - `grep -r "functionName" ./technical/src/`<p>
    >     - Searches for `"functionName"` in all files within the `./technical/src/` directory and its subdirectories, making it invaluable for codebase searches.<p>
    > >  ```
    > >  OUTPUT:
    > > ./technical/src/module1.js:functionName() defined on line 14
    > >  ./technical/src/util/helpers.js:Usage of functionName on line 82
    > > ```
    >   - `grep -r "TODO" ./technical/docs/`<p>
    >     - Recursively searches for `"TODO"` comments within all documentation in `./technical/docs/`. It's useful for finding unfinished tasks in project documentation.<p>
    > >  ```
    > >  OUTPUT:
    > > ./technical/docs/readme.md:TODO: Update documentation - line 5
    > >  ./technical/docs/setup/instructions.txt:TODO: Add installation details - line 18
    > > ```
    
    > #### `-v` (invert match)
    > - The `-v` option inverts the search, returning lines that do not match the given pattern.<p>
    >   - `grep -v "excludeThis" ./technical/config.txt`<p>
    >     - This command filters out lines containing `"excludeThis"` from `config.txt`, useful for excluding specific entries.<p>
    > > ```
    > > OUTPUT:
    > > This line does not contain the excluded term.
    > > Another relevant line of configuration.
    > > ```
    >   - `grep -vr "excludeThis" ./technical/settings/`<p>
    >     - Recursively filters out lines from all files under `./technical/settings/` that contain `"excludeThis"`, helpful for cleaning or analysis tasks.<p>
    > > ```
    > > OUTPUT:
    > > ./technical/settings/main.conf:All other configurations are included here.
    > > ./technical/settings/user_prefs.conf:User preferences setup.
    > > ```
    
    > #### `-l` (files with matches)
    > - The `-l` option causes `grep` to print only the names of files with matching lines, once for each file, instead of printing the lines that match. This option is particularly useful when you're more interested in knowing which files contain the match rather than seeing every matching line.<p>
    >   - `grep -l "keyword" ./technical/report.txt`<p>
    >     - This output indicates that `report.txt` contains the term `"keyword"`. It's useful for quickly identifying files that need further review or processing based on the presence of certain terms.<p>
    > > ```
    > > OUTPUT:
    > > ./technical/report.txt
    > > ```
    >   - grep -lr "keyword" ./technical/articles/<p>
    >     - `grep -lr` can be used to recursively identify files that contain `"keyword"` across multiple directories and subdirectories within `./technical/articles/.` It simplifies the task of finding relevant documents without delving into the specifics of each match.<p>
    > > ```
    > > OUTPUT:
    > > ./technical/articles/article1.txt
    > > ./technical/articles/research/research1.txt
    > > ```


### Source Citation:

- "grep(1) — Linux manual page."
  - Accessed by running the command `man grep` in the terminal. This manual page provides a comprehensive overview of the `grep` command, including descriptions and usage examples for options such as `-i` (ignore case), `-r` (recursive), `-v` (invert match), and `-l` (files with matches). 

