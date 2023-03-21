# Breizh CTF theme

Breizh CTF theme is based on [core-beta](https://github.com/CTFd/core-beta) original theme.
Breizh CTF theme aims to be used with "dynamics" scoring challenges and custom tags to provide a difficulty hint for the player. The following tags are available:

- `Very easy` / `Très Facile`
- `Easy` / `Facile`
- `Medium` / `Moyen`
- `Hard` / `Difficile`
- `Very hard` / `Très Difficile`

## Install and Build

### Install

Simply go to your theme folder and run `git clone https://git-bzh.alfred.cafe/breizh-ctf-2023/ctfd-theme-breizhctf-2023`. You can now select the `breizhctf` in the administration section.

### Edit / Build

You can edit files located in `assets` or `template`.
To compile file located in `assets`, go to theme folder "breizhctf" and run the following commands:

```bash
npm i
yarn install
yarn build
```

If you want a continuous build while editing, opt for:

```bash
npm i
yarn install
yarn dev
```