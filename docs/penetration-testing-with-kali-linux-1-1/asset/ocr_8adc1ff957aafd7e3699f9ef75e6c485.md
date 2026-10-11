# *Listing 281 - Running dirb against www.megacorpone.com.*

According to the output in Listing 281, DIRB made 4,612 requests and reported the URL, status code, and size of nine distinct resources. By default, the tool will recurse into newly-discovered directories, but in this case, our non-recursive (-r) scan simply reports directories without descending into them. Obviously, we could begin with a non-recursive scan against a large target and recursively search interesting directories, or begin with a full recursive scan depending on our needs.

> DirBuster is a Java application similar to DIRB that offers multi-threading and a GUI-based interface.

# 9.3.3 Burp Suite

Burp Suite$^{244}$ is a GUI-based collection of tools geared towards web application security testing, arguably best-known as a powerful proxy tool. While the free Community Edition mainly contains tools used in manual testing, the commercial versions include additional features, including a formidable web application vulnerability scanner. Burp Suite has an extensive feature list and is worth investigation, but we will only explore a few basic functions in this section. Please note that while Burp Suite Professional is prohibited during the OSCP exam, it is also not necessary.

Let’s start Burp Suite. We can find it in Kali under **Applications** > **03 Web Application Analysis** > burpsuite.

$^{244}$ (PortSwigger, 2019). https://portswigger.net/burp