# ## Testing FreeBSD

Each version and release of FreeBSD is tested in a variety of ways. Individual developers check their work on their own hardware and ask each other to double-check their work. If the work is sufficiently complicated, they might use the official FreeBSD Phabricator system (*https://reviews.FreeBSD.org/*) or even a private source code repository to offer their work to a broader community before committing it to -current. Analysis companies have donated analysis software to the FreeBSD team so that the source code can be automatically audited, tested, and debugged on an ongoing basis, catching many errors before they have a chance to affect real-world users. Corporations such as Sentex, EMC, Netflix, and iX Systems provide testing for the Project. Several highly regarded FreeBSD developers have made testing a major issue within the Project. They now have an automated Kyua testing framework.

Ultimately, however, a volunteer project with a few hundred developers can’t purchase all computer hardware ever made, nor can they run that hardware under all possible loads. The FreeBSD Project as a whole relies on companies and people that use FreeBSD to test the software.

The most useful testing comes from users who have real-world equipment and real-world testbeds with real-world workloads. Sadly, most of these users perform testing when they put a release CD into the computer, run an install, and fire up the system. At that point, it’s too late to benefit the release. Any bugs you find might help the next release, but in the meantime, a patch might fix your problem.

The solution here is obvious—test FreeBSD on your real-world workloads before the release is cut. Requests for testing of new -stable releases appear on *FreeBSD-stable@FreeBSD.org*. By testing a -stable or -current, you’ll get even better value from FreeBSD.

# ## Which Version Should You Use?