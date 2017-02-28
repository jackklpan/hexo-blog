---
title: mac pyenv install fail due to lib
tags:
  - python
date: 2015-10-17 22:05:00
---

zipimport.ZipImportError: can't decompress data; zlib not available
<div>
</div><div>https://github.com/yyuu/pyenv/issues/451</div><div>
</div><div>successful installed by</div><div>

    CFLAGS="-I$(brew --prefix openssl)/include -I$(xcrun --show-sdk-path)/usr/include" \
    LDFLAGS="-L$(brew --prefix openssl)/lib" \
    pyenv install -v 3.5.0`</pre>
    And actually it can be fixed when installed
    <pre style="background-color: #f7f7f7; border-bottom-left-radius: 3px; border-bottom-right-radius: 3px; border-top-left-radius: 3px; border-top-right-radius: 3px; box-sizing: border-box; color: #333333; font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace; font-size: 12px; line-height: 1.45; overflow: auto; padding: 16px; word-wrap: normal;">`xcode-select --install

</div><span style="font-family: Consolas, Liberation Mono, Menlo, Courier, monospace;">then directly&nbsp;pyenv install xxx</span>