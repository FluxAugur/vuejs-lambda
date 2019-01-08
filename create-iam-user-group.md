## Set Up an Admins Group

1. Create and name group
2. Attach policy granting administrative permissions
3. Add at least one user to group

To find out the minimum required arguments for a command using the AWS CLI, you can add the option --generate-cli-skeleton and you will receive json output of what is needed to successfully run that command.

To create a group, we provide the group name, and an optional [Path](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-friendly-names). We will redirect the output of our command to a json file so that we can reference various output artifacts.

```
$ aws iam create-group --group-name Admins --path /its/ > output/iam-create-group-admins.json
```

Our output should look similar to
```
{
  "Group": {
    "Path": "/its/",
    "CreateDate": ""
  }
}

While we can input our configuration data (as json) on the command line, it is much easier to store it in files and simply provide the file to our AWS CLI command.
