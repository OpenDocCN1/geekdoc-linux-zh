+   - Testing and monitoring
+   - Go to step 3 (results analysis)

This methodology might not work for everyone, but it is a good starting point. A number of tips and techniques that assure the effectiveness of this methodology are given in the sections that follow. Let’s look at the methodology in a little more detail.

# Step 1: Initial Assessment

The goal of step 1 is to understand the environment that you are evaluating. If you are tuning your own system, this step might be something that you are quite familiar with. If you have been brought in to tune someone else’s system, this might involve a little more work. In either case, it is useful to document your assessment of the system. These are some of the steps involved in the initial assessment:

+   - **Learn about the application** It is important that you have a basic understanding of the system and the application and how they work.
+   - **Ask about how it works and what it does** You should be able to find someone who can provide information about how the system operates, what the various components are, and how they interact.
+   - **Determine what the reported problem is** If a problem has been reported, determine exactly what the reported problem is. Often the reported problem is “everything is slow.” Getting more details could help the process.
+   - **Document database size, tuning parameters, etc.** Before you start tuning the system, you should document the size of the database, Oracle and Linux parameters, etc.
+   - **Validate parameters** Now and then, tuning problems are solved in the first few minutes of the engagement by finding an improperly set parameter. This is rare, but it does happen.

This is a very important stage of the tuning exercise, but the least glamorous. By getting your documentation and information lined up in the beginning, you might have already set in motion a successful project.

# Step 2: Monitor the System

The goal of this phase is to monitor the system and gather data. This data can then be used to develop a theory of what might be causing the performance problems that you are experiencing. As with step 1, it is important to document your results