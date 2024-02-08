# Lab Report 3

## Part 1 - Bugs

Choose one of the bugs from week 4's lab.

Provide:

- A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)
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
- An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
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
- The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
  - > <img width="1003" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/09081abf-652d-4be7-8c7f-8d437dd22f99">
    > <img width="1003" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/6753846a-85d9-4fd6-b2e0-c701b74d4fc0">

- The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
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
    >     int temp = arr[I];
    >     arr[i] = arr[arr.length - i - 1];
    >     arr[arr.length - i - 1] = temp;
    >   }
    > }

- Briefly describe why the fix addresses the issue.
  - > The fix addresses the issue by correctly swapping the elements in place. It does so by only iterating halfway through the array (up to `arr.length / 2`) and using a temporary variable (`temp`) to hold the value of the element being moved. This ensures that each pair of elements (one from the start and one from the end) is swapped exactly once, without overwriting any values prematurely. 

- Consider the commands less, find, and grep. Choose one of them. Online, find 4 interesting command-line options or alternate ways to use the command you chose. To find information about the commands, a simple Web search like “find command-line options” will probably give decent results. There is also a built-in command on many systems called man (short for “manual”) that displays information about commands; you can use man grep, for example, to see a long listing of information about how grep works. Also consider asking ChatGPT!

For example, we saw the -name option for find in class. For each of those options, give 2 examples of using it on files and directories from ./technical. Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.

That makes 8 total examples, all focused on a single command. There should be two examples each for four different command-line options. Many commands like these have pretty sophisticated behavior possible – it can take years to be exposed to and learn all of the possible tricks and inner workings.

Along with each option/mode you show, cite your source for how you found out about it as a URL or a description of where you found it. See the syllabus on Academic Integrity and how to cite sources like ChatGPT for this class.


