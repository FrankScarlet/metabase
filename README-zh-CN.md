# README

## Zen

**The Zen of Metabase**


- Give the user value as soon as possible

- Structure things so that we can automagically infer things for the user

- Don’t ask the user for information the system should already know

- Make it easy for the user to do the right thing

- Don’t leave the user booby traps

- Go the extra mile to make the user experience pleasant 


## 语言包

~~I am Chinese!(大雾)~~

所以语言包(`locales.clj`)只需要编译简体中文就行了。

有一个错误

```bash
Step "Build translation resources" failed with error "Compiling locales/nl.po for frontend...\n+ Warning: removed 8 fuzzy translations\n./bin/i18n/build-translation-resources: 43: msgfmt: not found"
# Ubuntu 20.04 WSL2 
# 看起来 msgfmt是个命令 但是找不到
sudo apt install gettext
# which msgfmt
# 问题解决
```
