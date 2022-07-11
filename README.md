# aws-secrets-manager-replicate
Replicate AWS Secrets on a host containing an AWS credentials file with all the required target profiles

#### Intended Audience
* Devops

#### Pre-requisites
* Jenkins host which containes an attached EC2 profile, permissioned across all target accounts via a trusted role
* An ./aws/credentials file containing all account profiles to allow script 'profile' call via AWS CLI to each target account, respectively
* A callable JSON file containing a list of all target accounts
* Secrets pre-populated in each target account's us-east-1 region

#### ./aws/credentials sample file
The sample below assumes each 'role_arn' is a role with trusted permissions to the Jenkins EC2 profile. Notice the 'credential_source' value, 'Ec2InstanceMetadata', indicating the EC2s attached profile will be used for authenticating to the target accounts.

**Example**
```
[profile accountA]
role_arn = arn:aws:iam::012345678910:role/target-role
credential_source = Ec2InstanceMetadata

[profile accountB]
role_arn = arn:aws:iam::012345678911:role/target-role
credential_source = Ec2InstanceMetadata

[profile accountC]
role_arn = arn:aws:iam::012345678912:role/target-role
credential_source = Ec2InstanceMetadata
```

### Callable JSON Account List
The sample below contains a list of target accounts in which the secrets should be replicated.

**Example**
```
   {
   "team.accountA": "012345678910",
   "team.accountB": "012345678911",
   "team.accountC": "012345678912",
  }
```

#### Usage
M

#### Example
* The latest major release 1 of the Devops repo, as supplied by the Foobar developer repo v1.2.3
  * i.e., Foobar v1.2.3 Yes

#### Active Choices Reactive Parameter script
```
def proc = "/bin/bash /var/lib/jenkins//iac_release_parser/iac_release_parser.sh ${git_repo_url} ${git_release} yes".execute()
proc.waitFor()
def output = proc.in.text
def exitcode = proc.exitValue()
def error = proc.err.text
return output.tokenize()
```
