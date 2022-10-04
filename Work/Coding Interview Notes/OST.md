##### General Optimizing Techniques from Interview Walkthrough:

  1. Look for unused information. How can you leverage that?
  2. Use a fresh example
  3. Solve it incorrectly. Think about why that solution isn't perfect and find the corrections.
  4. Make time vs. space tradeoff. Storing extra state can optimize runtime.
  5. Precompute information. Can reorganizing data like sorting or computing values up front save time?
  6. Use a HASH TABLE.
  7. Think about best conceivable runtime.

### Optimize and Solve Techniques

#### Technique #1: Look for BUD:

B: Bottlenecks
U: Unnecessary Work
D: Duplicated Work

###### Bottlenecks:

- Part of algorithm slowing overall runtime.
  1. One-time work that slows down algorithm
    - Look for task or area in code that takes biggest O time in algorithm
  2. Repeated work that can be reduced
    - Double check any work that is repeated to see if you can reduce runtime here

###### Unnecessary Work:

- Check to see if there's any steps from brute force and later optimized algorithm that we can immediately say will reduce work in some way
- Even if it doesn't affect your big O, it may take you a step in the right direction to actually reducing it
- Write out why it reduces work then analyze that reasoning to see if there is even more unnecessary work
  - e.g. if you say there's only one value that will work for a variable given the others, you may still be looping for that final variable, but you could be solving using a derivation of the given calculation

###### Duplicated work:

- Look for situations where you are computing the same values multiple times for another loop. These values can be stored in a hash map/table and used later.
- Consider if you may additionally be storing data for the other loop in the hash map already if you are making comparisons. How could you find the solution from here without more unnecessary work?

#### DIY 

- When you get a question, think about working through it intuitively with a real-life example. Often your intuition works better than "designing an algorithm". 
- Works well when considering combinations or permutations.
- Use a nice big example and manually solve the problem for that example. Reverse engineer your own approach into an algorithm then optimize from there.
  - Be aware of any "optimizations" your brain intuitively made and note those when creating the algorithm.

#### Simplify and Generalize

- First, simplify or tweak some constraint e.g. data type.
- Then, solve simplified.
- Finally, adapt/generalize simplified solution to the more complex problem.
  - Often this step will involve using more complex data structures than the simplified answer

#### Base Case and Build

- First solve the problem from a base case, then build up from there.
- When reaching more complex/interesting cases (often n=3 or 4), we try to build those using the prior solutions.
- These will often lead to natural recursive algorithms

#### Data Structure Brainstorm

- Simply run through a list of data structures and try to apply each one
- Example structures
  - Linked list
    - Not good at accessing/sorting numbers
  - Array
    - Keeping elements sorted as their added is expensive
  - Binary tree
    - Does well with ordering
  - Heap 
    - Great a basic ordering and keeping track of max and mins

#### Best Conceivable Runtime (BCR)

- Literally best runtime you could conceive of a solution to a problem having
  - Easily proven by considering the work that needs to be done/what needs to be looked at

- Same as Best Case Runtime, but for a problem not an algorithm
  - Largely a function of inputs and outputs
    - Don't assume just because you need elements are distinct that you need to look at all of them
  - Don't compute by thinking about what your algorithm does!!
 
- Not necessarily achievable, just know can't do better than it

- Start with example, then brute force, then BCR to find bounds

- Don't assume runtime is a multiple choice question
  - There are common runtimes, but don't assume runtime just from sheer process of elimination
  - If confused and want to take a guess, most likely non-obvious runtime

Helpful for:
a. BCR can get a hint for what is needed to be reduced from brute force to get closer to it
b. Any work done that's less than or equal to BCR is "free", in that it won't impact runtime
  - May want to eliminate eventually but not a priority
c. Tells us "Done" with optimizing runtime, so turn to space complexity
  - Consider other algorithms that don't use extra space (alternatives to hash tables)
  - Now you can use BUD to find bottleneck
d. If you reach BCR and have O(1) additional space, then you know you can't optimize time or space

#### Overall Process/Steps:
  1. Write example for question
  2. Consider a brute force algorithm and its runtime
  3. Consider your best conceivable runtime
    - Keep in mind you should consider input and output in the problem, not potential algorithms
  4. Consider what theoretical runtimes your optimal algorithm could have
    - Don't assume it's a common one!
  5. Consider both your brute force and BCR runtimes to see which part can be reduced to get them closer
  6. Consider optimization techniques at top of this file.
    - One-time work with runtime less than BCR is "free"
  7. Consider space complexity and if any other algorithms can use less extra space (often not using a hash table)
  8. Given such an algorithm, attempt to optimize the runtime to reach the BCR
    - Consider specific details of the problem, for example sorting

Once the BCR and minimal space (O(1) additional space) are achieved, we know we can't optimize big O time or space.