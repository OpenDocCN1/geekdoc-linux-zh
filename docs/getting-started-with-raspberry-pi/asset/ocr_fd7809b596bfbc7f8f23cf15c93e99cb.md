# # Build Scripts

Customers generally ask for periodic software builds during the development cycle. Each build includes new features or bug fixes. The deliverables for an embedded PC derivative, for example, may include firmware components such as the base kernel, loadable device driver modules, filesystem utilities, bootloader, BIOS, and on-card microcode. To automate build generation, it’s a good idea to implement a set of versatile build scripts that obtain a source code snapshot from the version control repository and generate a packaged deliverable.

Listing 22.1 shows a skeletal build script that assumes use of CVS for version control. This is a simple script that shows only the kernel build. In the real world, you might need a sophisticated suite of scripts that package several software components and manage different installation scenarios.

# ## Listing 22.1. A Simple Build Script

```
Code View:
# Check that compilation tools are installed
#...

# Assume that $user contains the user name, $cvsserver contains
# the CVS server name and /path/to/repository is the location
# of your project's repository on the CVS server
CVS="cvs -d :pserver:$user@$cvsserver:/path/to/repository"
$CVS login

# Check-out the kernel
$CVS checkout kernel

# Build the kernel
cd kernel
make mrproper
#Get the .config file for your platform
cp arch/your-arch/configs/your_platform_defconfig .config
make oldconfig
make -j5 bzImage # Accelerate by spawning 5 instances of 'make'
if [ $? != 0 ]
then
    echo "Error building Kernel. Bailing out.."
    exit 1
fi

# Copy the kernel image to a target directory
cp arch/x86/boot/bzImage /path/to/target_directory/productname.kernel

# Build modules and install them in an appropriate directory
make modules
if [ $? != 0 ]
then
    echo "Error building modules. Bailing.."
    exit 2
fi

export INSTALL_MOD_PATH=»$TARGET_DIRECTORY/modules»
make modules_install

# Rebuild after forcing generation of identical MD5 sums and
```