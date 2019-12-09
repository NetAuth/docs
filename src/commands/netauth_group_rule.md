## netauth group rule

Alter group rules

### Synopsis


The rule command manages rules for groups.  Rules can be a powerful
tool to make your server's memberships easier to manage, but care
should be taken to ensure your rules remain maintainable.  The rules
system will ensure that cycles are not introduced to the membership
graph, but no checks are performed for the sanity of the rules
requested or the maintainability of the resulting graph.  Rules
require the membership tree to be parsed for entries at all levels,
and use of rules should be carefully weighed against the performance
requirements of your organization.

There are two types of rules in NetAuth: INCLUDE and EXCLUDE.  Both of
these rules take a target to act on and are applied to a single group.
In writing, group rules should be formatted as <RULE>:target.  For
example INCLUDE:sub-group.

The INCLUDE rule does exactly what the name implies.  Members of the
target group gain membership in the named group without being added to
it directly.  This rule is convenient for building up organizational
trees where you might want to translate some easily explainable
relation into a group membership.  For example the group "eng" might
include all members of "dev" and "ops".  By adding these exansions the
membership of "eng" is kept up to date without additional effort.

The EXCLUDE rule is slightly more complicated.  Members of the target
group are excluded from membership in the source group even if they
are otherwise directly members.  This can be useful if you have a need
to prune out some memberships without removing groups from
individuals.  For example if you have contractors that can't access
production data but otherwise need to be members of groups that grant
such access, you could create a new group "production-data" that gates
this access and has an rule of EXCLUDE:contractors where "contractors"
contains all contractor owned users (possibly even via includes).
This would allow you to maintain groups that make sense to humans
while still removing people from groups they shouldn't logically be
in.

Removing a rule can be done by using the DROP keyword.  This keyword
allows you to target a rule by target group and remove it.


```
netauth group rule <group> <INCLUDE|EXCLUDE|DROP> <target> [flags]
```

### Examples

```
$ netauth group rule example-group include example-group2
Nesting updated successfully

```

### Options

```
  -h, --help   help for rule
```

### Options inherited from parent commands

```
      --config string   Use an alternate config file
      --entity string   Specify a non-default entity to make requests as
      --secret string   Specify the request secret on the command line
```

### SEE ALSO

* [netauth group](netauth_group.md)	 - Manage groups and associated data

###### Auto generated by spf13/cobra on 8-Dec-2019