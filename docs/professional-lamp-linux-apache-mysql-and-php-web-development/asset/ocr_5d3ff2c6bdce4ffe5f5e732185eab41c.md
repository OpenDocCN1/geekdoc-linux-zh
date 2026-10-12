# # 12
# Caching Engines

You’ve done your best to clean up your code and reduce processing load in your PHP scripts, but you just can’t seem to make your pages fast enough to keep your users happy. Time to throw in the towel? Not quite—there’s more performance you can get out of your LAMP setup, and caching engines will help you do this.

When dealing with different caching solutions for PHP5, you have a handful of choices. A couple of setups actually cache the internally compiled PHP scripts, others cache the generated output, and others still cache the intermediate data processing objects. This chapter introduces you to several caching engines, and can help you decide which one is right for you.

# ## Alternative PHP Cache

Alternative PHP Cache, or APC, is a PHP opcode caching engine, now provided for free as part of the PECL/PEAR repository. APC originated with Daniel Cowgill and George Schlossnagle, and was released by Community Connect, Inc. After the release of PHP5, Yahoo! modified APC to support the new Zend Engine, and it has since become part of PECL.

APC works by taking the compiled code from the PHP runtime engine and storing it in shared memory for later access. Each time a script is downloaded, APC checks for a version in shared memory first, before recompiling and executing the script that resides on disk. Because PHP doesn’t need to recompile the script each time, it can greatly speed up the response time—speed increases of over four times or greater can be obtained in some situations.

APC can be installed as either a dynamic shared object (DSO), or built into PHP statically. The following section shows you how to install the DSO version, as it doesn’t require you to recompile PHP, and provides the flexibility to add or remove the DSO at will.