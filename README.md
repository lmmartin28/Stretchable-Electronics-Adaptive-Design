# Stretchable-Electronics-Adaptive-Design
This repository provides code to simulate and analyze stretchable systems with microstructured conductivity variations, modeling their electrical response under strain using advanced resistance calculations, shortest-path optimizations, and microstructure design algorithms for improved computational efficiency.For reference to published work please see:

Louis Martin-Monier et al. ,Novel insights into the design of stretchable electrical systems. Science Advances .7,eabf7558(2021).
https://www.science.org/doi/10.1126/sciadv.abf7558

**Framework** 

The substrate in this model is represented as a matrix, where isolated regions of high conductivity (such as particles, lines, or circles) are embedded within a lower conductivity background. When the system undergoes uniaxial strain, the microstructure is deformed, and the connectivity between the conductive regions changes, altering the system's electrical properties.

**Effective Medium Resistance vs Actual Resistance**

The code highlights the difference between effective medium resistance and actual resistance. The effective medium resistance represents an average value of the system’s conductivity, treating the substrate as a homogeneous material. However, this model diverges from the actual resistance, which accounts for the specific microstructure and geometry of the system. The divergence between these two models becomes most apparent closer to the percolation threshold, where small changes in the distribution of high-conductivity regions lead to large shifts from insulating to conducting states. This transition is critical to understanding how resistance behaves as the substrate is deformed and how microstructural properties influence the overall electrical performance.

**Microstructure Variations and Strain-Dependent Resistance**

The code defines various microstructures to assess how the resistance evolves under strain. These microstructures consist of different shapes, sizes, and patterns of high-conductivity regions within the substrate. The code calculates the system’s resistance for different levels of strain, allowing users to observe how the electrical properties of the system change as it deforms. This is key to understanding how structural design impacts resistance, particularly in stretchable electronics or sensors.

 **Voltage Grid Calculation Methods**

Two primary methods are used to calculate the voltage grid across the microstructured substrate:

-**Gauss Elimination (time complexity O(N^3))**: This is a direct method that solves the system of equations governing the voltage distribution. It involves matrix inversion, which is computationally expensive, particularly for larger systems. While this method provides exact solutions, its computational complexity grows rapidly as the system size increases, making it inefficient for large-scale simulations.

-**Gauss-Seidel red-black ordering (time complexity O(N^2))**: This is an iterative solver that updates voltage values in a checkerboard pattern. Although it is more efficient than Gauss elimination, it still requires a significant amount of computation, especially as the system scales. This method converges to an approximate solution over multiple iterations, but it remains computationally intensive, particularly for large and complex microstructures.

While both methods provide useful results, neither is particularly efficient when the matrix size increases, leading to high computational costs as the system size grows. These methods are suitable for smaller systems but become impractical for large-scale simulations due to their increasing time complexity.

**Shortest Path Optimization for Efficient Calculation**

To reduce the computational load associated with calculating the voltage and current distribution across the substrate, **Dijkstra’s algorithm (time complexity O(N log N))** is employed to find the shortest path between two points. The shortest path represents the route of least resistance that current would follow between two points (e.g., two electrons). By identifying and focusing on these shortest paths, the algorithm significantly reduces the number of paths that need to be considered for voltage and current calculations. This selective approach helps avoid solving for the entire matrix, which can be computationally expensive, particularly for large systems.

Once the shortest path is identified, **Yen's K-shortest path algorithm (time complexity O(K.N log N))** is used to compute a set of K shortest paths between two points. These K paths capture alternative routes for current flow through the substrate. By considering multiple paths, this method provides a more comprehensive and accurate representation of the system's resistance-strain response. It is especially useful for understanding how different microstructural configurations and conductivity variations affect the overall electrical performance under strain.

Together, Dijkstra’s algorithm and Yen’s K-shortest path algorithm help optimize the simulation by focusing on the most critical conductive paths. This allows for an efficient and scalable calculation of the system’s electrical properties, making it possible to model larger and more complex systems without the computational burden of solving for all voltage and current values across every possible connection.

**Optimization Algorithm for Microstructure Design**

Finally, an **optimization algorithm** is used to explore different microstructure geometries and architectures. Given a **target resistance-strain response**, this algorithm **iterates over various microstructure configurations and conductivity ratios** to find the best combination that achieves the desired performance. This approach helps design substrates with tailored electrical properties, optimizing the balance between conductivity and mechanical deformation.

In summary, the repository provides a comprehensive framework for simulating and analyzing the electrical behavior of stretchable substrates with complex microstructures. The code’s focus on shortest path algorithms—particularly Dijkstra’s and Yen’s K-shortest paths—is a crucial element for improving computational efficiency, enabling the simulation of larger, more complex systems. These methods allow the system to focus on the most critical current paths, drastically reducing the computational load compared to traditional matrix-based methods like Gauss elimination and checkerboard iterative update, which become inefficient as the system scales up. This makes the code ideal for exploring the design of stretchable electronics and systems that require precise control over their electrical responses under strain.
