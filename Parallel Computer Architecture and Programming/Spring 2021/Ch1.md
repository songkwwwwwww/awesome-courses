Lecture 1: Why Parallelism? Why Efficiency?
--------




Course theme1: Designing and writing parallel programs ... that scale

- Parallel thinking
    1. Decomposing work into pieces that can safely be performed in parallel
    2. Assigning work to processors
    3. Managing communication/synchoronization between the processor so that it does not limit speed up
- Abstraction/mechanisms for performing the above tasks
    - Writing code in popular parallel programming languages

Course theme2: Parallel computer hardware implementation: how parallel computers work
- Mechanisms used to implement abstractions efficiently
    - Performance characteristics of implementations
    - Design trade-offs: performance vs. convinience vs. cost
- Why do I need to know about hardware?
    - Because the characteristics of the machine really matter
    (recall speed of communication issues in earlier domos)
    - Because you care about efficiency and performance
    (you are writing parallel programs after all!)

Course theme3: Thinking about efficiency
    - Fast != Efficient
    - Just because your program runs faster on a parallel computer, it does not mean it is using the hardware efficiently
        - is 2x speedup on computer with 10 processors a good result?
    - Programmer's perspective: make use of provided machine capabilities
    - HW designer's perspective: chhosing the right capabilities to put in system
    (performance/cost, cost = silicon area?, power?, etc.)

Course theme4: 










