# M4 Configuration File: Sendmail.mc

For years, administrators had to struggle with the sendmail.cf file by hand to get it to do what they wanted. There was no standard or default way to make changes easily. Eventually, computers became much faster, and SMTP was standardized. So, starting with version 8 of Sendmail, a set of macros for the m4 macro language were written to make it easy to create, modify, and maintain all the common configurations for the sendmail.cf file. The file that contains these macros is called an mc file.

The sendmail.mc for Caldera OpenLinux 2.2 follows. This file is used to generate the gigantic sendmail.cf that you just finished looking over. As you can see, it is considerably smaller and somewhat easier to understand (though you certainly wouldn't call it easy). Basically each of the options in the sendmail.mc file is tied to a specific set of rules and option lines in the sendmail.cf file. So if you set an option in sendmail.mc, it will be used to change all that relevant information in the sendmail.cf. An excellent reference for each of the options is included in /usr/share/sendmail/cf/README if you are interested in working with this by hand.

```
```/usr/share/sendmail/cf/cf/generic-col2.2.mc
divert(0)
#
# Copyright 1996, 1997 Caldera Inc., Provo
#
divert(-1)
#
# THIS SOFTWARE IS PROVIDED BY Caldera AND CONTRIBUTORS ``AS IS'' AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL Caldera OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS
# OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT
# LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
# OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
# SUCH DAMAGE.

divert(0)dnl
#
# This is a generic configuration file for Caldera OpenLinux 2.2
#
# Basic ideas taken from Red Hat contrib/sendmail-8.7.5-1.src.rpm.
# Credits go to Marc (whatever built it). 
#
VERSIONID(`$Id: generic-col2.2.mc,v 1.4 1999/02/23 15:36:07 okir Exp $')
divert(:1)
OSTYPE(`linux')
```