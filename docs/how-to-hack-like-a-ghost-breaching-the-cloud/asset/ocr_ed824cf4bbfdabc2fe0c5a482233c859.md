```
AccessKey: {
    UserName: elis.skyler,
    AccessKeyId: AKIA44ZR K6WSRDLX7TDS,
    SecretAccessKey: 564//eyApoe96Dkvo0EdgAwroe lak78eghk
```

Using these new credentials, we request temporary AWS keys belonging to the OrganizationAccountAccessRole:

```
root@Point1:~/# aws sts assume-role \
--role-session-name maintenance \
--role-arn arn:aws:iam::345673068670:role/OrganizationAccountAccessRole \
--profile elis \
--duration-seconds 43 200
```

```
AccessKeyId: ASIAU6EUDNIZIADAP6BQ,
SecretAccessKey: xn37rimjEAppjDicZZP19hOhLuTo2P06SXZxeHbk,
SessionToken: FwoGZXlVYXdzEGwa...
```

That was not so hard after all. Okay, let's use these access credentials to look up the AWS Secrets Manager in this new account:

```
root@Point1:~/# aws secretsmanager list-secrets \
--region eu-west-1 \
--profile it-role
```

```
ARN: arn:aws:secretsmanager:eu-west-1: 345673068670:secret:it/
gsuite-apps/user-provisionning-40YxPA

Name: it/gsuite-apps/user-provisionning,
--snip--
```

Brilliant. We fetch the secret's content and decode it to retrieve the JSON file used to authenticate Google service accounts (see Listing 13-5).

```
root@Point1:~/# aws secretsmanager get-secret-value \
--secret-id 'arn:aws:secretsmanager:eu-west-1:345673068670:secret:it/ \
gsuite-apps/user-provisionning-40YxPA' \
--region=eu-west-1 \
--profile it-role \
| jq -r .SecretString | base64 -d
```

```
{
    "type": "service_account",
    "project_id": "gp-gsuite-262115",
    "private_key_id": "05a85fd168856773743ed7ccf8828a522a00fc8f",
    "private_key": "-----BEGIN PRIVATE KEY-----... ",
    "client_email": "userprovisionning@gp-gsuite-262115.iam.gserviceaccount.com",
    "client_id": "100598087991069411291",
--snip--
```

Listing 13-5: Retrieving the GCP service account key