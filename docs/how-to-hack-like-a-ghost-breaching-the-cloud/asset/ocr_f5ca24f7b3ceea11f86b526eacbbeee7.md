Machines cannot follow this authentication flow, so Google also provides service accounts that can authenticate using private keys. Yet, when looking at the source code, we do not find the slightest hint of private keys:

```
root@Point1:~/it-gsuite-apps/# grep -Ri "BEGIN PRIVATE KEY" *
root@Point1:~/it-gsuite-apps/#
```

> NOTE
*The caveat is that service accounts can only be defined on Google Cloud Platform. So, in effect, to use Google Workspace properly, one needs to subscribe to GCP as well. Of course, this is mentioned nowhere in the docs, so you just magically land on the GCP platform from a Google Workspace window.*

So, we dive into the code of it-gsuite-apps to understand how the app acquires its Google Workspace privileges and stumble upon the lines shown in Listing 13-2.

```
--snip--
getSecret(SERVICE_TOKEN);
--snip--
public static void getSecret(String token) {
    String secretName = token;
    String endpoint = "secretsmanager.eu-west-1.amazonaws.com";
    String region = "eu-west-1";

    AwsClientBuilder.EndpointConfiguration config = new AwsClientBuilder.
EndpointConfiguration(endpoint, region);
--snip--
```

*Listing 13-2: A code excerpt that loads a service token from AWS Secrets Manager*

Now it makes sense. The secret is not hardcoded in the app but retrieved dynamically through Secrets Manager, an AWS service for centralizing and storing secrets. We don’t have the secret’s name, but lucky for us, we have full admin privileges, so we can easily search for it:

```
root@Point1:~/# aws secretsmanager list-secrets \
--region eu-west-1 \
--profile rundeck

"Name": "inf/instance-api/api-token",
"Name": "inf/rundeck/mysql/test_user",
"Name": "inf/rundeck/cleanlog/apikey",
"Name": "inf/openvpn/vpn-employees",
--snip--
```

Unfortunately, no amount of grepping reveals anything remotely related to Google Workspace. We manually inspect every entry just in case, but the hard reality quietly dawns on us: the IT department must be using another AWS account. That’s the only rational explanation.

No need to panic, though. Hopping over to the IT AWS account will not require the same stunt we pulled when jumping from MXR Ads to GP.