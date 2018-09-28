Objective:

Write a program that prints out a multiplication table of the first 10 prime number.
1) The program must run from the command line and print one table to
STDOUT.
2) The first row and column of the table should have the 10 primes, with each
cell containing the product of the primes for the corresponding row and
column.

Notes

1) Consider complexity. How fast does your code run? How does it scale?
2) Consider cases where we want N primes.
3) Do not use the Prime class from stdlib (write your own code).

Developer Notes:

I tackled the tedious work formatting of the table first, saving the fun math for last. My first test stubbed the 'primes' method with a more manageable sized array that would still present the same formatting issues. The next test was actually created after getting the table working with ten primes, and is there to test the proposed use case. The next test confirms the class generates the expected values for ten primes. The last two tests are to see how well the system scales to 1000 and 5000. I didn't do any formal timing profiling, but the run time for the tests on my system were ~.1 second and ~2.5 seconds for 1000 and 5000 respectively. When I increased the n value to 10000 for the last test, the run time was >10 seconds, which suggests a big-O factor of n squared dominating with larger n. 

I assumed that for the purpose of the exercise I would be expected to show a method of calculating the primes as opposed to just using a hard-coded list. I used the 'Sieve of Eratosthenes', which is the most intuitive and straightforward implementation of a sieve, and performs well for smaller values of n. Generally, a sieve is an algorithm that starts with all the numbers up to a certain limit, and eventually discards all the non-prime values. The 'calculate_primes' and 'next_prime' method implement the sieve.

One of the difficulties with implementing a sieve is knowing how many numbers to start with. That is, what is the upper bound on the nth prime number. I found a proof I sort of understood that n squared is an upper bound. However, n squared is a lot of numbers to work with. I found an article that was well-reviewed with a function closer to n(log n) for an upper bound. I implemented that function in 'upper_limit' (along with a method 'ln' to make it a little more readable).

This solution would not scale well for n in the thousands or greater. I did try to make sure the really expensive calculations were only performed once. Beyond the obvious optimization of relying on a list of known primes, some optimizations to consider for the purpose of scaling would be: 

1) note that the table of calculated values is symmetric about the diagonal and could be stored using half the memory and generated with just half the calculations.
2) The mathematics are beyond me but I understand there are sieves with better performance for greater values of n. I used Eratosthenes because it's easy to understand and implement, and is fine for smaller n.
3) the initial calculation of the primes takes a lot of memory. I understand there are methods to limit the size of the sieve, but they would make the implementation more complex.
