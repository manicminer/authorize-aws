# AWS Security Group Authorizer

This is a straightforward script which detects your current public IP address, inspects the specified AWS security group to see if your IP address matches a rule entry, and adds/replaces rules as necessary.

By default the script will assume you want to grant yourself SSH access (TCP/22) and will use your local system username as the rule description. When `-D` is given, any existing rules with the same description are removed _if_ the script deems it necessary to create a new rule, otherwise existing rules are left alone.

## Requirements

Uses Python 3.6 and Boto 3. Run `pip install -r requirements.txt`. A suitable Python version manager is recommend, but you can install as root if you really want to.

## Example usage

```
# Create a new rule in the employees security group
authorize-aws -g employees

# Create a new rule as above, and delete any existing rule with your name on it
authorize-aws -g employees -D

# As above, but using a different AWS profile than the default one
authorize-aws -p acme -g employees -D

# Use a different AWS region
authorize-aws -r us-west-2 -g employees

# For Windows instances
authorize-aws -g employees -t 3389

# By default, the description contains your local user name, but can be overridden
authorize-aws -g employees -d 'Carmen mobile'
``
