# Hamlet, an email corpus

This repository contains randomly generated emails according to our
[`mrmime`][mrmime] tool. Mr. MIME is a library to parse & encode an email. So
we developped a tool to randomly generate an email and ensure a kind of
isormophism such as:
```sh
$ x = generate (seed)
$ test x = decode (encode (x))
```

This corpus contains **valid** emails and Mr. MIME does not alterate them when
it parses or encodes them. Our MUA should do the same! As the
[Enron's corpus][enron], Hamlet wants to improve the email stack.

## How to reproduce Hamlet

This corpus was generated via our Mr. MIME tool with a specific seed. You can
reproduce the generation:
```sh
$ git clone https://github.com/mirage/mrmime
$ cd mrmime
$ opam pin add -y .
$ dune exec corpus/generate.exe -- crowbar --multi 1000000 --seed 0
```

## Isomorphism

We don't compare strictly generated email and encoded/decoded email but we
assume that they should have the same structure (e.g. `multipart`), headers
should be the same (`Content-Type`, `Content-Transfer-Encoding` or `Date`)
and contents should be the same.

By this way, semantically, Mr. MIME does not alterate your email and what you
parsed is what you can read.

## License

The corpus is under the CC0 license.

[mrmime]: https://github.com/mirage/mrmime
[enron]: https://www.cs.cmu.edu/~enron/
