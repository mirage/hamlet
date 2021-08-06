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

The equality we have defined between a generated email `m` and its and decoded
counterpart `m'` is not strictly exact. What is actually check is:

- _structural equality_: both emails must have the same structure. For example,
if `m` is a multipart email with 3 parts, `m'` is also a multipart mail with 3
parts, and the equality is recursivly called on each of the parts;

- _partial header equality_: the headers present are the same and in order but
equality between the values is only checked for the headers for which values are
completely parsed by `mrmime` (like `Content-Type`, `Content-Transfer-Encoding`
or `Date`). Note a small exception for `Content-type` header: `boundary`
parameter can change between `m` and  `m'`;

- _content equality_.

By this way, semantically, Mr. MIME does not alterate any important
part of your email and what you parsed is what you can read.

## License

The corpus is under the CC0 license.

[mrmime]: https://github.com/mirage/mrmime
[enron]: https://www.cs.cmu.edu/~enron/
