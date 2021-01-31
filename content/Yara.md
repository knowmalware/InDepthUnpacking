# Yara

## General

- Be aware of dependencies
- Modules
- Regex works differently in v2+

## Various sources of rule sets

- http://yararules.com/
- http://www.deependresearch.org/2012/08/yara-signature-exchange-google-group.html
- https://github.com/kevthehermit/YaraRules

## Organizing your rules

- Private
- Tags
- Metadata
  - author - name and contact info
  - date - yyyy-mm-dd
  - description - what does this rule do
  - reference or source - link to blog, whitepaper reference, etc.
  - sample - file hashes
- C-style comments
- Normalization (e.g. [yaratool](https://github.com/chrislee35/yaratool))

## Sharing your rules

**DO NOT** use external variables without being VERY explicit that they are required and an example of how to run Yara with providing appropriate values to them.

**DO NOT** use lots of external variables.
