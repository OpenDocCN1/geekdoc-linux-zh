This extracts the package files into a folder named `sh tool-2.0.8`. Use the `cd` command to change to the newly created folder:

		`cd shtool-2.0.8`

Now you're ready to build the shell script library file.

# # Building the library

The shtool distribution file must be configured for your specific Linux environment. To do that, it uses standard `configure` and `make` commands, commonly used in the C programming environment. To build the library file, you just need to run two commands:

		`$ ./configure`
		`$ make`

The `configure` command checks the software necessary to build the shtool library file. As it finds the tools it needs, it modifies the configuration file with the proper paths to the tools.

The `make` command runs through the steps to build the shtool library file. The resulting file (`shtool`) is the full library package file. You can test the library file using the `make` command as well:

		`$ make test`
		Running test suite:
		echo........ok
		md4te.......ok
		table.......ok
		prop........ok
		move........ok
		install.....ok
		mkdir.......ok
		mklm........ok
		mkshadow....ok
		fixperm.....ok
		rotate......ok
		tarball.....ok
		subst.......ok
		platform....ok
		arx.........ok
		slo.........ok
		scpp........ok
		version.....ok