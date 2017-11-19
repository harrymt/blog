---
layout: post
title: 1.1 Million SLOC
---

<div class="message">
I have contributed 1.1 Million Source Lines of code (SLOC) to open-source.
</div>

My <a href="//github.com/harrymt">GitHub profile</a> shows all my contributions. I used the the following command to calculate the SLOC:

This command prints lines of code for all source repos (not forks):

```bash
$ curl https://api.github.com/users/harrymt/repos | \
  jq '.[] | {name: .name, fork: .fork, sloc: .languages_url}' | \
  grep -B 2 -A 2 '"fork": false' | \
  grep 'sloc' | \
  cut -d '"' -f 4 | \
  xargs -L 1 curl | \
  sort | awk '{sum += $2} END {print sum}'
```

Note: this command requires jq:
```bash
$ sudo apt-get install jq
```

This will give you the total sum of SLOC for each repo on GitHub for the user `harrymt`:

3.4 Million (3,412,411)

To get a language by language breakdown remove `sort | awk '{sum += $2} END {print sum}'`

e.g.
```
curl https://api.github.com/users/harrymt/repos | \
  jq '.[] | {name: .name, fork: .fork, sloc: .languages_url}' | \
  grep -B 2 -A 2 '"fork": false' | \
  grep 'sloc' | \
  cut -d '"' -f 4 | \
  xargs -L 1 curl
```

Results in (after manually merging):

```
"C": 752,454
"C++": 15,404
"CSS": 23,313
"HTML": 194,733
"Java": 148,768
"JavaScript": 106,832
"Makefile": 81
"Makefile": 962
"Matlab": 44,085
"Perl": 1510
"Python": 1,769,616
"Ruby": 50
"Shell": 547
"SQLPL": 330,425
"TeX": 14,227
"TypeScript": 9404
```

However, this doesn't neccessarily contain generated code or libraries. Therefore, I have manually estimated libraries LOC by going over each repo:


Breakdown:

```
"Python": 519,616
"JavaScript": 106,832
"HTML": 124,733
"C": 102,104
"Java": 100,768
"Matlab": 44,085
"CSS": 23,313
"C++": 15,204
"TeX": 14,227
"TypeScript": 9,404
"Makefile": 1,241
"Shell": 547
"Perl": 110
```


Total:
1.1 Million (1072184)

We can see that one repo contained over 1 million lines of Python library files.

My top languages, continue to be more front-end, Python, JavaScript and HTML. Interesting that I have more SLOC in HTML than CSS.

Counted on 19/11/2017
