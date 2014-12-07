- Start Date: 2014-09-17
- RFC PR: (leave this empty)
- Rust Issue: (leave this empty)

# Summary

This is a _conventions_ RFC for formalizing the basic conventions around
documenting Rust code.

# Motivation

Documentation is an extremely important part of any project. It's important
that we have consistency in our documentation.

For the most part, the RFC proposes guidelines that are already followed today,
but it tries to motivate and clarify them.

# Detailed design

Full and complete documentation for any Rust project should include the following:

1. A high-level, informal overview (a 'guide')
2. In-depth, cross-cutting topic-level documentation (other 'guides')
3. API documentation

`rustdoc` is able to produce all three kinds of documentation, and should be used
for all Rust documentation.

First, we'll talk about each type of documentation individually, and then cover
styles that are common across all three kinds of documentation.

## The Guide

A "guide" is an entry point into your project. As such, it should be written at
a high level, and not dig too deep into the details. To learn more, a reader
can consult the other documentation.

A `README.md` file often serves as a guide for many Rust projects, but this
role can also be served by a separate document.

The guide should cover:

* Installing your project.
* If it is a library, example lines to place in your `Cargo.toml`.
* An overview of features your project includes.
* Basic usage of your project.

After reading a guide, your user should have a basic grasp on what your library
is, what it does, and how to use it.

Your guide should point users to other documentation for more details where
appropriate.

## Guides

Depending on your project's size, additional guides may be appropriate.
Individual guides work well for cross-cutting concerns in your library. Any
concepts which span multiple modules are good fit for a guide.

## API documentation

Good API documentation is key for using your library. Here are guidelines when
writing API documentation:

Avoid block comments. Use line comments instead:

```
// Wait for the main task to return, and set the process error code
// appropriately.
```

Instead of:

```
/*
 * Wait for the main task to return, and set the process error code
 * appropriately.
 */
```

Only use inner doc comments `//!` to write crate and module-level
documentation, nothing else.

Within doc comments, use [Markdown](https://en.wikipedia.org/wiki/Markdown)
to format your documentation.

Use top level headings `#` to indicate sections within your comment. Common
headings include 'Arguments,' 'Examples,' and 'Failure'.

The first line in any doc comment should be a single-line short sentence
providing a summary of the code. This line is used as a short summary
description throughout Rustdoc's output, so it's a good idea to keep it short.

All doc comments, including the summary line, should begin with a capital
letter and end with a period, question mark, or exclamation point. Prefer full
sentences to fragments.

The summary line should be written in [third person singular present
indicative](http://en.wikipedia.org/wiki/English_verbs#Third_person_singular_present)
form. Basically, this means write "Returns" instead of "Return".

## Common Style Guidelines

All documentation is standardized on American English.

Use graves (\`) to denote a code fragment within a sentence.

Use triple graves (\`\`\`) to write longer examples, like this:

    This code does something cool.

    ```
    let x = foo();
    x.bar();
    ```

When appropriate, make use of Rustdoc's modifiers. By default, triple graves will
make the assumption that Rust code is contained within. For anything that's not
Rust code, annotate it with the proper name.

    ```ruby
    puts "Hello"
    ````

References and citation should be linked inline. Prefer

    [some paper](http://www.foo.edu/something.pdf)

to

   some paper[1]

   1: http://www.foo.edu/something.pdf

## Testing embedded code

Rustdoc is able to test all Rust examples embedded inside of documentation. This is why we encourage fully runnable examples, for example:

    ```rust
    fn main() {
        println!("Hello Rust!");
    }
    ```

Mark all `rust` examples as `rust`, as this eases work for third-party markdown parsers/highlighters.

To further describe your code, you can use additional tags. Use the extended tag syntax for multiple tags:

    ```{.rust .no_run}
    fn main() {
        // Some very expensive computation
    }
    ```

Use the following tags to further refine things:

* `should_fail`: Treat failure of the code snippet as success and vice versa.
* `no_run`: Compile the snippet, but don't run, e.g. for costly operations.
* `ignore`: Highlight as Rust, but otherwise ignore the full snippet
* `test_harness`: Wrap tests in one module.

It is important to mark what is not Rust so your tests don't fail. For example, shell code can be highlighted as:

    ```sh
    echo "Hello sh!"
    ```

There used to be a `notrust` flag, which is now discouraged.

# Drawbacks

None.

# Alternatives

Not having documentation guidelines.

# Unresolved questions

None.
