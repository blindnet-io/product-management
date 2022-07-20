# Lost password reset procedure

| Status      | accepted
| :---------- | :-------------------------------------------------------------------------------------- |


## Context and Problem Statement

How can we offer lost password reset while keeping e2ee principle as much as we can ?


## Considered Options

- option 1: Client can just change password with account email address : email address, forms links are kept but data is lost
- option 2: Client can have one (or more) trusted contacts who have half the secret S and we, blindnet, have half the secret S which is used to derive the key K. K is used decrypt client's private key. There is security tradeoff if blindnet and trusted contact ally against client to decrypt his data
- option 3: The reset can be done via other devices on which client is already logged in so he can transfer the keys
- option 4: Blindnet stores key, which breaks e2e principle and zero trust 

## Decision Outcome

- For the moment we go for **option 2 trusted contact option** (cf. Facebook lost password process uses trusted contacts)
- We should have a **baseline** which we default to if reset password process failed or user do not set up the reset password process. The **option 1** of changing password with account email address (email address, forms links are kept but data is lost) is our baseline

## Working documents : 
- [Figma diagrams and sketches](https://www.figma.com/file/G7Fm7WiOecw3n7MScbtSL9/Lost-password-reset?node-id=0%3A1) 

## History <!-- optional -->

- Product dev issue [#182](https://github.com/blindnet-io/product-management/issues/182)
- Product dev issue [#129](https://github.com/blindnet-io/product-management/issues/129)


<!-- markdownlint-disable-file MD013 -->
