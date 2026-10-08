# Table 5-3 Computational Libraries to Link, by Function Domain

| Function domain | IA-32 Architecture | Intel® 64 or IA-64 Architecture |
| --- | --- | --- |
| | Static | Dynamic | Static | Dynamic |
| BLAS, CBLAS, Sparse BLAS, LAPACK, VSL, FFT, Trigonometric Transform, Functions, Poisson Library | libmk_core.a | libmk_core.so | libmk_core.a | libmk_core.so |
| Iterative Sparse Solvers, Trust Region Solver, and GMP routines | libmk_solver.a or libmk_solver_sequential.a | n/a | See below | n/a |
| Iterative Sparse Solvers, Trust Region Solver, and GMP routines | libmk_core.a | n/a | libmk_solver_lp64.a or libmk_solver_lp64_sequential.a | n/a |
| LP64 interface | n/a | n/a | libmk_solver_ilp64.a or libmk_solver_ilp64_sequential.a libmk_core.a | n/a |
| Direct Sparse Solver/PARDISO* Solver | libmk_core.a | libmk_lapack.so libmk_core.so | libmk_core.a | libmk_lapack.so libmk_core.so |