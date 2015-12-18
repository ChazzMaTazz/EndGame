This file exhbits all the traits of

```ruby
  APP_TYPES = [
    RAVE_MODULES,
    SLAAD,
    JANUS,
    RAVE_ARCHITECT_SECURITY,
    RAVE_ARCHITECT_ROLES,
    RAVE_X,
    RAVE_EDC,
    JUNO
  ]

  MATCHERS_TYPES = {
    /gambit|RaveX(?! )/i => RAVE_X,
    /RaveX? EDC$/i => RAVE_EDC,
    /RaveX? Modules$/i => RAVE_MODULES,
    /slaad|Labs/i => SLAAD,
```
