# Hacking Custom Web Applications • Chapter 11

# Note

This chapter is authored by members of SensePost's research and development team. What follows therefore is SensePost's methodology for assessing and analyzing custom-built Web applications.

SensePost is an independent and objective organization specializing in IT security consultancy, training, and assessment services. SensePost is situated in South Africa from where it provides services to more than 50 large global clients. SensePost's Information Security Management Systems (ISMS) division consists of a team of qualified BS7999 Lead Auditors assisting organizations with the problem of defining their security infrastructures and the management processes required for successful information security implementation across all areas of organization. Visit www.sensepost.com or e-mail info@sensepost.com.

Using a well defined methodology ensures a consistent and repeatable process of assessment. Often, we find that analysts can get caught up in a single piece of a puzzle that they fail to look at the bigger picture, or as the proverb goes, they can't see the forest for the trees. A methodology ensures that despite distractions, all possible avenues for attack have been explored. SensePost's Web application testing methodology is outlined in the following list. This methodology makes sense for a single form or section of an application. Automating these techniques is covered later in the chapter, as well as problems associated with this automation. This methodology is expanded throughout the chapter.

+   - Use the source. Much information can be hidden in the HTML source, from developer comments to hidden fields.

+   - Locate possible interactivity. You need to find those aspects of the application/form that interact with the end user.

+   - Pinpoint the attack vectors. Before begins with understanding what the application was designed to, and understanding what one can make it do.

+   - Execute and examine. This phase involves actually launching an attack, and determining whether or not the attack was successful.

![](bbox=[0.706, 0.943, 0.927, 0.966])