# DaWanda RuboCop configuration

This contains common RuboCop settings that should be inherited from by all
other projects using RuboCop. Changes to this repository will be picked up
automatically by other projects using it.

Specific project-level settings should be kept to a minimum.

## Installation in a new project

Put this at the top of the `.rubocop.yml`:

```yaml
inherit_from:
  - https://raw.githubusercontent.com/dawanda/rubocop-config/master/rubocop.yml
```

_The raw URL will stop working if this repository is made private._

This will download the configuration file and cache it in the root directory of
the project, we probably want to `.gitignore` this:

```
.rubocop-https---raw-githubusercontent-com-dawanda-rubocop-config-master-rubocop-yml
```

### Code Climate

Code Climate does not allow RuboCop to download the configuration by itself,
but it does allow fetching files in a prepare-step. If we download the file
with the same (complicated) name that RuboCop would download it as, RuboCop
simply thinks it already did that and uses that config correctly.

Doing this lets us continue to use the 24h caching that RuboCop does in
development, but also always have the most up to date version in CI without
ever manually updating the file.

In the `.codeclimate.yml`

```yaml
prepare:
  fetch:
  - url: "https://raw.githubusercontent.com/dawanda/rubocop-config/master/rubocop.yml"
    path: ".rubocop-https---raw-githubusercontent-com-dawanda-rubocop-config-master-rubocop-yml"
```
