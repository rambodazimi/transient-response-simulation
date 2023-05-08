# transient-response-simulation
Simulation of transient response of a circuit in MATLAB

The primary goal of this project is to simulate the transient response for a provided circuit. The approach to simulating the transient response of this circuit is to solve the Modified Nodal Analysis (MNA) equations shown in Equation 1 and the compact form in Equation 2. Hence, we are going to compute the transient response for all the voltage nodes, namely, V1, V2, and V3.

We aim to identify the most effective technique for accurately and efficiently solving the non-linear system of equations. The choices of the algorithm were made in terms of practicality of approach and efficiency, so all approaches use the Newton-Raphson method, with added uses of the forward, backward Euler and trapezoidal rules. We aim to check for relative accuracy and CPU cost when using these three in addition to the N-R method. The separate approaches and testing solutions are described in detail in the following report.

## APPROACH 1 - Newton-Raphson Method in conjunction with the Forward Euler Method
In the first approach, we solved the MNA equations using a popular method called the Newton-Raphson Method for N variables. Newton-Raphson method can be used to solve the system of non-linear equations of N variables. It attempts to find roots with an iterative approach, meaning that we

   
Start from an initial guess (initial condition) and then use the Jacobian matrix to refine our guess until a desired level of accuracy is achieved. Assume we have a system of N equations.

In order to implement the Newton-Raphson algorithm in Matlab, we form the system of equations using the equation shown in Equation 1 and set the initial conditions and values as follows.
𝐴 = 5;𝑓𝑟𝑒𝑞𝑢𝑒𝑛𝑐𝑦 = 60;𝑤 = 𝑠*𝑝𝑖*𝑓𝑟𝑒𝑞𝑢𝑒𝑛𝑐𝑦;𝑥0 = [0;0;0;0];𝑡𝑜𝑙 = 1𝑒−6 After setting the values properly, we call the method newton_raphson_system with valid arguments. Then, we simulate the results obtained from the method and plot the result in the time interval [0s, 0.5s]. After implementing the Newton-Raphson method, it is time to apply the Forward Euler method to provide accurate solutions to systems of nonlinear equations.

## APPROACH 2 - Newton-Raphson Method with Trapezoidal Rule
The second approach used involved using the Newton-Raphson method as described in approach 1 with the use of the trapezoidal rule. This method combines the benefits of both methods to provide accurate solutions to systems of nonlinear equations. In this method, the trapezoidal rule is used to approximate the integral of the function, which is then used to compute the function's derivative. The derivative is then used in the Newton-Raphson method to update the solution estimate. The Newton-Raphson method with the trapezoidal rule has several advantages over other numerical methods. First, it is a fast and efficient method that can provide accurate solutions to complex problems. Second, it is a robust method that can handle various functions and equations. Third, it is a flexible method that can be adapted to suit different types of problems and situations. Finally, it is a widely used method that has been extensively studied and validated.

Xguess or X0 has been modified to represent an accurate initial value for all terms of X. The rest is mainly testing and plotting the output results. That is done in terms of plotting all # voltage functions, V1(t), V2(t) and V3(t) in terms of t(s). 

## APPROACH 3 - Newton Raphson Method with Backward Euler
The third approach we developed begins with the Newton-Raphson method. It is similar to the method used for approach 1, where a set of MNA equations is solved using the Newton-Raphson method coupled with the forward Euler method. In this approach, we concurrently use the backward Euler method to solve the equations produced as an output of the Newton-Raphson method instead. The method used may also be described as follows.
The backward Euler method involves approximating the derivative of the solution at each time step using the backward difference formula. This results in a system of nonlinear equations that can be solved using the Newton-Raphson method. The Newton-Raphson method involves linearizing the system of equations and solving the resulting linear system using matrix operations. Using the Newton-Raphson method with backward Euler can provide a highly accurate solution for nonlinear ODEs, but it may require more computational resources than other numerical methods.
To apply the Newton-Raphson method with backward Euler, we first use the backward Euler method to generate an initial guess for the solution at the next time step. We then linearize the ODEs around this guess and use the resulting linear system to compute a correction to the guess using the Newton-Raphson algorithm. We then repeat this process, using the corrected guess to generate a new linear system until we obtain a sufficiently accurate solution. The resulting plots obtained for the voltage and time can be observed in Figure 3. These are in terms of all three output voltages found, namely V1(t), V2(t), and V3(t), as also described in the previous approaches.

## TESTING
The testing for all three approaches was completed by plotting the transient responses in terms of V1(t), V2(t) and V3(t) against t for all three approaches used. This gives us a firm set of figures that can be used to categorically determine which of our functions works best concerning the required problem. Regarding general expectations, the Forward Euler method is the cheapest regarding CPU cost, requiring only one function evaluation per time step. The Newton-Raphson and the Backward Euler methods require a nonlinear equation's solution at each time step, making them more computationally expensive. The Trapezoidal rule falls somewhere in between, requiring two function evaluations per time step.
However, it is essential to note that the cost of an algorithm is highly dependent on the specific problem being solved and the desired level of accuracy. Higher-order methods tend to be more accurate than lower-order methods, meaning the trapezoidal rule provides more accurate results than the Forward or Backward Euler. This is imminent when comparing figures 1, 2 and 3 as figure 2 is the most in line with expected results, and theoretical expectations make it our approach of choice.
Moreover, to aid our determination of the most efficient method, we can compare the time it takes for each method to solve the system. Hence, we use “tic” and “toc” to measure the time in each implementation. We run each algorithm multiple times and calculate the average time for each implementation.

Approach 1 (N-R with Forward Euler): Elapsed time is 0.2092078 seconds.

Approach 2 (N-R with Trapezoidal): Elapsed time is 0.0.2161832 seconds.

Approach 3 (N-R with Backward Euler): Elapsed time is 0.2094102 seconds.

## TEAM CONTRIBUTIONS
All three members worked individually on the implementation and documentation for each approach. Furthermore, Rambod focused more on the introduction and design sections for the report, while Ahmad focused more on the testing and conclusion portions, and Trevor worked on the presentation.

## CONCLUSION
In conclusion, we used three approaches to solve the problem. We prioritized accuracy among our three approaches as CPU cost is approximately equal for all approaches, which was most clearly seen when using the Newton-Raphson method in cooperation with the trapezoidal rule. So that is the approach we have chosen for our final implementation, and the code and the description of the used approach have been described in our submission.
