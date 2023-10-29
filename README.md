# HHL-Algorithm

There are 5 stages involved in HHL algorithm:
- Loading the data:
$$\ket{0}<sub>nb</sub>  \rightarrow \ket{b}<sub>nb</sub> $$

- Applying QPE:
If we let U act on $\ket{b}$ : 
$$U\ket{b}=U\left(\sum_{j=0}^{N+1}  b_{j} \ket{u_{j}}\right) $$
$$= \sum_{j=0}^{N+1}  e^{i\lambda_{j}t} \ket{u_{j}} \bra{u_{j}} \left(\sum_{j=0}^{N+1}  b_{j} \ket{u_{j}}\right)$$
$$= \sum_{j=0}^{N+1}  b_{j} e^{i\lambda_{j}t} \ket{u_{j}}$$
Then, using quantum phase estimation, we can find the quantum state $\ket{\lambda_{j}}$ of $\lambda_{j}$. The quantum state of the register expressed in the eigenbasis of A is now
$$ QPE(\sum_{j=0}^{N+1}  b_{j} \ket{0}<sub>nl</sub> \ket{u_{j}}<sub>nb</sub>) = \sum_{j=0}^{N+1}  b_{j}\ket{\lambda_{j}}<sub>nl</sub> \ket{u_{j}}<sub>nb</sub>$$


- Use of auxiliary qubits 
Controlled rotation operation is done on auxiliary qubit conditioned on $\ket{\lambda_{j}}$ for eigen value inversion,
$$\sum_{j=0}^{N+1}  b_{j}\ket{\lambda_{j}}_{nl}\ket{u_{j}}_{nb}\left(\sqrt{1-C^2/\lambda_{j}}\ket{0}+C/\lambda_{j}\ket{1}\right)$$
where C is a normalisation constant. 

- Applying inverse QPE 
The inverse of quantum phase estimation gives us the following.
$$\sum_{j=0}^{N+1}  b_{j}\ket{0}<sub>nl</sub> \ket{u_{j}}<sub>nb</sub> (\sqrt{1-C^2/\lambda_{j}}\ket{0}+C/\lambda_{j}\ket{1})$$
- Measuring auxiliary qubit 
Measure the auxiliary qubit, and if $\ket{1}$ is measured, then we get
$$\left(\sqrt{\frac{1}{\sum_{j=0}^{N+1}  |{b_{j}}|^2/|{\lambda_{j}}|^2}}\right)\sum_{j=0}^{N+1} \frac{b_{j}}{\lambda_{j}}\ket{0}<sub>nl</sub>\ket{u_{j}}<sub>nb</sub>$$
which up to a normalisation factor corresponds to the solution


For the system of equations -
$$x - \frac{1}{4}y = 4$$
$$-\frac{1}{4}x + y = 0$$
The above system of equations can be represented in matrix form as follows :

$$ \begin{bmatrix} 1 & -\frac{1}{4} \\\ -\frac{1}{4} & 1\end{bmatrix} \begin{bmatrix}x \\\ y \end{bmatrix} = \begin{bmatrix} 4 \\\ 0 \end{bmatrix}$$
The above system of equation can be solved by Gaussian elimination method as follows, \\
$$x - \frac{1}{4}y = 4$$
$$\frac{15}{16}y = 1$$

We get the solution x = $\frac{64}{15}$, y = $\frac{16}{15}$ 
which is exactly the same as the solution that one can get by NumPy solver.

The HHL algorithm offers a speed up over the fastest classical algorithm for solving system of linear equations provided the linear system is sparse and has a low condition number 
$\kappa$ , and that the user is interested in the result of a scalar measurement on the solution vector, instead of the values of the solution vector itself. 

HHL Algorithm working principle:
To solve a simultaneous linear equation with a quantum algorithm, we need to map $A\vec{x}=\vec{b}$ to a quantum circuit. In order to do that we have to normalize the vectors. By re-scaling the system, we can assume $\overrightarrow{b}$ and $\overrightarrow{x}$ to be normalised and map them to the respective quantum states $\ket{b}$ and $\ket{x}$. The problem now becomes,
$$A\ket{x}=\ket{b}$$ 
It's essentially a quantum matrix inversion problem. This problem can be efficiently solved in quantum computer by obtaining the following equation as an output,
$$\ket{x}=A^{-1}\ket{b}$$
Assumptions of HHL :
- matrix A is Hermitian
- Hamiltonian simulation and solution functions can be computed
- Condition number of a A is well behaved.

Since A is hermitian, it can be represented in it's eigenbasis.Then A can be expanded using the eigenvector $ \ket{u_{j}}$ and it's eigenvalue $\lambda_{j}$ as follows.

$$ A = \sum_{j=0}^{N+1} \lambda_{j} \ket{u_{j}} \bra{u_{j}} $$

Therefore, the inverse matrix is as follows.

$$ A^{-1} = \sum_{j=0}^{N+1} \lambda_{j}^{-1} \ket{u_{j}} \bra{u_{j}} $$

Since $\ket{u_{j}}$ is an eigenvector of A, $\ket{b}$ can be represented by its superposition

$$ \ket{b} = \sum_{j=0}^{N+1} b_{j} \ket{u_{j}} \bra{u_{j}} $$

In the end, we would like to obtain the following equation as the output,

$$ \ket{x} = A^{-1}\ket{b} = \sum_{j=0}^{N+1} \lambda_{j}^{-1} b_{j} \ket{u_{j}} $$




### References

https://en.wikipedia.org/wiki/Quantum_algorithm_for_linear_systems_of_equations
https://qiskit.org/textbook/ch-applications/hhl_tutorial.html

