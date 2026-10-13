# Quiz Answers

+   1. The correct answer is D. Believe it or not, all the rest can be guessed relatively casually by commonly available software.
+   2. The correct answer is C.
+   3. The correct answer is B.
+   4. The correct answer is D. If you're on the Internet, you *must* be on guard!
+   5. The correct answer is E.

# Exercises

+   1. Install `tcpflow` (available in the ports in `/usr/ports/net/tcpflow`); use it to see if any cleartext traffic is being sent to and from your machine, aside from Web traffic and SMTP (which generally requires no passwords). What potential problems can you foresee facing an administrator as a result of using this program? Why might you choose to use `tcpdump` (which only prints out packet headers, rather than the entire packet) instead? Hint: It's an ethical question.
+   2. Design a scheme by which to generate random passwords for new users. One example is to use `md5 -s` to create a hash string from a bunch of randomly pressed input characters; you can take the first seven letters from that hash output and use it as a random initial password for each user.
+   3. Use the `pkg_version` utility to determine which of your installed ports are out of date. Make sure to synchronize your ports tree first!

![](bbox=[0.88, 0.15, 0.99, 0.33])