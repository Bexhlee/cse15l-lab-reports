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
    > public void testReverseInPlaceFailure() {
    >   int[] original = {1, 2, 3, 4};
    >   ArrayExamples.reverseInPlace(original);
    >   assertArrayEquals(new int[]{4, 3, 2, 1}, original);
    > }
    > ```
- An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)
  - > An input that doesn't induce a failure for the `reverseInPlace` method could be an empty array or an array with a single element,
    > as the logic flaws in the method won't affect such arrays.
    >
    > Here's a JUnit test for such a scenario:
    > ```java
    >@Test
    > public void testReverseInPlaceNoFailure() {
    >   int[] original = {1};
    >   ArrayExamples.reverseInPlace(original);
    >   assertArrayEquals(new int[]{1}, original);
    > }
    > ```
- The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)
  - > The symptom of running the failure-inducing test would be a failed test, indicating that the expected array after reversal does not match the actual array.
    > <img width="1003" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/09081abf-652d-4be7-8c7f-8d437dd22f99">


  
- The bug, as the before-and-after code change required to fix it (as two code blocks in Markdown)
- Briefly describe why the fix addresses the issue.

