## Set Up an Admins Group

1. Create and name group
2. Attach policy granting administrative permissions
3. Add at least one user to group

To find out the minimum required arguments for a command using the AWS CLI, you can add the option --generate-cli-skeleton and you will receive json output of what is needed to successfully run that command.

### Create Group

To create a group, we provide the group name, and an optional [Path](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-friendly-names). We will redirect the output of our command to a json file so that we can reference various output artifacts.

```
$ aws iam create-group --group-name Admins --path /its/ > output/iam-create-group-admins.json
```

Our output should look similar to the following.
```
{
  "Group": {
      "Path": "/its/",
      "GroupName": "Admins",
      "GroupId": "AGPAJ3JNXXHK4OTWHWIHI",
      "Arn": "arn:aws:iam::096188391785:group/its/Admins",
      "CreateDate": "2019-01-08T01:45:18Z"
  }
}
```

Note that the GroupId is created and assigned by AWS, and that the Arn includes your account number.

The Amazon Resource Name (ARN) format is required by some services. Other services allow you to use friendly names.

```
arn:partition:service:region:account:resource
```

Let's list all of our groups just to verify that our Admins group was created successfully.

```
$ aws iam list-groups
```

Our output should list a collection of Groups containing only our Admins group currently.

### Attach Policy to Group

We will allow any user in the group to perform any action on any resource in the AWS account by attaching an [AWS Managed Policy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html) called AdministratorAccess to the Admins group.

Read more about [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) and policies.

```
$ aws iam attach-group-policy --group-name Admins --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

If the command is successful, there is no response. List group policies attached to the Admins group to confirm the command's success.

```
$ aws iam list-attached-group-policies --group-name Admins
```

You can confirm the contents of a particular policy with the get-policy command.

```
$ aws iam get-policy --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

### Add User to Group

Now we'll add the user we created in the console to the group we created with the AWS CLI.

```
$ aws iam add-user-to-group --user-name some-user --group-name Admins
```

Again, if this command is successful, there is no output. We can check the command's success by listing the groups for our user.

```
$ aws iam list-groups-for-user --user-name some-user
```

#TODO
- Add section on creating users with AWS CLI (and various concerns) [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
- Add information on tagging resources [here](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html)
