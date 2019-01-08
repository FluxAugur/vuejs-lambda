### Create an Everyone users group.

```
$ aws iam create-group --group-name Everyone --path /its/ > output/iam-create-group-everyone.json
```

### Allow Users to Manage Own Passwords

Only from the [My Password page](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_user-change-own.html) in the console.

#### Create Policy

```
$ aws iam create-policy --policy-name allow-users-to-manage-own-passwords-from-mypassword-page --policy-document file://source/json/iam-policy-allow-users-to-manage-own-passwords-from-mypassword-page.json > output/iam-create-policy-allow-users-to-manage-own-passwords-from-mypassword-page.json
```

#### Attach to Everyone group

```
$ aws iam attach-group-policy --group-name Everyone --policy-arn arn:aws:iam::096188391785:policy/allow-users-to-manage-own-passwords-from-mypassword-page
```

#TODO
- Other policies [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_delegate-permissions_examples.html#creds-policies-credentials)
-
