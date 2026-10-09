The Apache group PGP signatures are in the file `KEYS` in the top-level distribution of Apache. If you trust the site from which you obtained your distribution, you can add these keys to your own key ring. If you do not how to use PGP on your system, learn about it at `www.pgp.com`.

Each Apache source distribution is PGP signed and these signatures are stored in files with an `.asc` extension (for example, the signature for `apache_2_0_tar_gz` is stored in `apache_2_0_tar_gz_asc`). These can be used to check the validity of the distribution if you have added the `KEYS` file contents to your key ring.

The latest stable version of Apache does not have any known bugs; however, its capability to incorporate external third-party modules gives rise to a security issue: Can you trust a third-party module? People all over the world write many of the Apache modules. Make sure that you only use modules that are available on the official Apache Web site or registered in the Apache module registry located at `http://modules.apache.org/`.

![](bbox=[0.14, 0.42, 0.21, 0.47])

Never use experimental modules in your production sites. In fact, it is a good idea to determine which modules you really need, and then to configure and compile Apache accordingly. This way you have a smaller, faster server with potentially better security.

When configuring Apache, pay a great deal of attention to security configuration issues. The basic idea is to disable anything you do not use. This way, you are taking preventive security measures and are likely to reduce risks.

# # Choosing a Security Configuration

There are many ways you can configure Apache while enhancing your overall Web security. Before you can choose a configuration suitable for you, you need to develop a security policy and then choose a configuration suitable to meet your policy requirements. When it comes to security there is always a chance that you can overestimate the risks and become too paranoid or underestimate your security needs and keep things too open. In the sections below I discuss a few configurations that suit different environments.

# ## Security policy considerations

An administrative security policy identifies practices that are vital to achieving robust network security. If you do not yet have one, consider adding some of the following items to an administrative security policy as a start.