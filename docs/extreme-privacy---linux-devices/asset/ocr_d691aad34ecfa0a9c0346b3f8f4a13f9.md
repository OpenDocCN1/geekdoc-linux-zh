many domains which I use for specific purposes. For comparison, a domain and email hosting through Namecheap would start at $30 annually. **You do not need a custom domain at all in order to follow the rest of this book.** If you have no plans for obtaining VoIP service, you could probably skip this step entirely. I find it beneficial to bypass the fraud filters at most of the telephony providers, so I want everything configured before I need it. Let's proceed.

# Twilio VoIP Service

When an app or service advertises "Burner Phone", "Second Phone", "Second Line", or other enticing verbage, they do not actually provide a telephone number or telephony services. Almost all of them rely on a VoIP service called Twilio. Even MySudo provides access through Twilio. These companies purchase numbers and service through Twilio and upsell the service to you. What if we eliminated the middle man? You could create your own Twilio account, purchase a number, and possess service without any third-party involvement. This Do-It-Yourself option is easier said than done, but a very attainable task.

The first step is to create a new account at Twilio (twilio.com) from a desktop computer. This will be the most difficult part of this entire process. You must provide a name, email address, and phone number to Twilio as part of your registration. Twilio possesses strong fraud mechanisms in order to suspend accounts which seem suspicious. During the first tests of this strategy, my accounts were immediately suspended. I had provided a vague name, burner email address, and Google Voice number while connected to a VPN. This triggered the account suspension and I was asked to respond to a support email explaining how I would be using Twilio.

This began communication with two Twilio support personnel. While talking with customer service, I was advised that the VPN IP address was most likely the reason for the suspension. After providing a business name, "better" email address, and explanation that I would be using the product for business VoIP solutions, my account was reinstated. **If you get caught within this dragnet, I discourage you to let them know you are following the protocol in this book to establish VoIP services.** Twilio does not like me or my general audience. We are small individual customers compared to big businesses.

After you create your free account, it will be severely restricted. Individual Twilio employees will analyze your registration details and decide if you can be "upgraded" into a fully-functioning account. I think you will find your account restrictions lifted within an hour if you apply the following guidelines.

+   *   Provide your true first and middle name, especially if they are generic. In my experience, a true last name is not needed.

+   *   If you created a custom domain, as explained in the previous chapter, provide an email address associated with this domain. Privacy-themed addresses from Proton Mail, Tutanota, or masked providers will be flagged and the account will be suspended. Gmail and other free addresses will be heavily scrutinized (or blocked entirely).

+   *   If possible, register without protection from a VPN. I will explain VPN usage later, but this can be a trigger for all new accounts. Public Wi-Fi, such as a local library, usually works well.

+   *   The telephone number provided could be an existing VoIP number or any landline number to which you have access. If you have an old Google Voice number, this should work well.