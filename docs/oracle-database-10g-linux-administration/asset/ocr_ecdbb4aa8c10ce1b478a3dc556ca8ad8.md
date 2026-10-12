important thing to remember is always to test your 10g RAC before putting it into production!

# Oracle 10g RAC Help

So now you know enough to get you in trouble. This chapter was not designed to be a step-by-step installation guide. It is a deployment guide that should guide you while you are deploying Oracle 10g RAC.

If you run into trouble, and you probably will, you should begin with MetaLink. Oracle normally has a step-by-step guide for each platform available. You can also search on Linux and the version of 10g you are installing. This should return some hits. Most of the time, someone has already ran into the same issue and solved it.

Here are a few items to keep in mind before you actually start your 10g RAC installation.

+   Always check with your hardware vendor to make sure you have the certified/tested versions of drives and software before you begin.

+   Make sure you have the Linux networking configured before you begin any RAC installation. If you do not have the networking configured correctly, you will have a lot of problems.

+   If you can get Cluster Ready Services (CRS) installed and operating on all nodes, you have won half the battle. Do not proceed until CRS is functioning properly!

+   Make sure you size your shared storage properly. Most of the poorly performing Oracle RAC implementations I’ve seen did not have enough physical disk drives or used the wrong RAID type. Remember RAID 1+0 is the preferred RAID type for Oracle data files.

+   Remember to have fun. Whenever I get stressed out about a project, I usually end up making mistakes. If we learned to have fun and the job will normally take care of itself.

# Summary

The last chapter provided you with an overview of what RAC is and how it’s used. In this chapter, you were provided with a much more detailed view of how RAC is installed and configured. Oracle RAC is a very complex product that depends much more on system hardware than a stand-alone Oracle installation. When deploying RAC clusters, I usually warn the client that deploying RAC is about 40 percent deployment and 60 percent debugging. If you look at the deployment that way, you won’t be as stressed when things don’t go quite right. Just keep on trying and remember to pay attention to the details.