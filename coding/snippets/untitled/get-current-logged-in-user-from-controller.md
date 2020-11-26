# Get current logged in user from Controller

This is useful if you know you will have a logged in user and you get get the unique key for that account: 

```text
IPublishedContent member = Members.GetCurrentMember();

// Pass member key to mode

model.MemberKey = member.key
```

