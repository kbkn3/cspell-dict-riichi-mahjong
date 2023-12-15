# cspell-dict-riichi-mahjong

## Overview

Custom dictionary for [CSpell](https://github.com/streetsidesoftware/cspell).

This package is a custom dictionary for CSpell to support mahjong domain knowledge terms in Japanese notation.

If you believe that additional words should be included, please submit a pull request with the approval of two or more repositories.

Words that are specific to each product can be customized in `cspell.json` in the repository.

<details>
<summary>日本語</summary>
    
[CSpell](https://github.com/streetsidesoftware/cspell)用のカスタム辞書

このパッケージは麻雀のドメイン知識的な用語を日本語表記に合わせてCSpellで対応するためのカスタム辞書です。

必要と思われる単語追加のPRを歓迎します。

各プロダクト固有の単語はリポジトリ内の`cspell.json`でカスタムが可能です。
</details>

## Contents

The dictionaries included in this repository are as follows:

- [game](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/game.txt): Mahjong game terms
- [pro](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/pro.txt): Professional mahjong player's organization name and M-League team name
- [rule](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/rule.txt): Mahjong rules
- [yaku](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/yaku.txt): Mahjong yaku

<details>
<summary>日本語</summary>
    
当リポジトリに含まれる辞書は下記の通り。

- [game](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/game.txt): 麻雀ゲームの用語
- [pro](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/pro.txt): 麻雀プロ団体名とMリーグチーム名
- [rule](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/rule.txt): 麻雀のルール
- [yaku](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/.cspell/yaku.txt): 麻雀の役
    
</details>

## Prepare

1. Install this config as devDependencies.

    ```bash
    npm install -D cspell-dict-riichi-mahjong
    ```

2. Create cspell.json to match your repository.

    ```json
    {
      "version": "0.2",
      "language": "en",
      "import": ["cspell-dict-riichi-mahjong/cspell.json"],
      // Add repository-specific terms that are missing from existing dictionaries.
      "words": [
        "chii-nya!",
      ],
      "ignorePaths": ["node_modules/**"],
      "minWordLength": 4
    }
    ```

See [CSpell Docs](http://cspell.org/configuration/) for detailed CSpell configuration instructions.

## How to use CSpell

Consider 3 different methods of operation for your team.

- VScode extension
  - Pros: You can use it simply by installing an extension to VSCode.
  - Cons: Only the code you are editing will be spell checked, not the entire repository.
- CSpell-CLI
  - Pros: fast working
  - Cons: Not aware of spelling errors while coding.
- CSpell-ESLint
  - Pros:
    - WARN underlines on the editor
    - Can be implemented by adding to existing eslint configuration.
    - Underlines can be added to the dictionary for each repository via the editor's underlining quick-fix.
  - Cons:
    - `pnpm run lint` after adding CSpell system settings takes a long time.
- ~Github Actions~
  - Currently no machine users have been added to this repository, so it is not available for Github Actions. If requested, this will be addressed.

It is recommended that VSCode and CSpell-CLI be used together.
The use of CSpell-CLI and CSpell-ESLint together is deprecated due to their overlapping roles.

<details>
<summary>日本語</summary>
チームに合わせて3つの運用方法から選んでください。

- VScode 拡張機能
  - 長所： VSCode に拡張機能をインストールするだけで使用できる。
  - 短所： 編集中のコードのみスペルチェックされ、リポジトリ全体はチェックされない。
- CSpell CLI
  - 長所： 動作が速い
  - 短所： コーディング中にスペルミスに気づかない。
- CSpell-ESLint
  - 長所
    - エディタ上に WARN の下線が表示される
    - 既存の eslint の設定に追記すれば実装が可能
    - エディタの下線部クイックフィックスからリポジトリごとの辞書への追加が可能
  - 短所
    - CSpell 系の設定を追記したあとの`pnpm run lint`は時間がかかる
- ~Github Actions~
  - 現在、このリポジトリにはマシンユーザーが追加されていないため、Github Actionsで利用することはできません。要望があれば対応します。

VSCode と CSpell-cli は併用することを推奨します。
CSpell-cli と CSpell-ESLint の併用は役割が被るため非推奨です。
</details>

## Installation

### VScode extension

1. Install [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
2. Reload Window from `cmd + Shift + P`

[How to Use with VSCode Extension](https://github.com/kbkn3/cspell-dict-riichi-mahjong/blob/master/HowToUseWithVSCodeExt.md)

### CSpell CLI

1. `npm install -g cspell` or `npm install cspell`
2. Register npm-script.
   example:
    ```json
      "scripts": {
          "spellcheck": "pnpm cspell ./src --cache --no-progress --config ./cspell.json || exit 0",
          "spellcheck-all": "pnpm cspell ./src --no-progress --config ./cspell.json || exit 0"
      }
    ```

3. (Optional) If you want automatic spell checking on every commit, consider installing [husky](https://github.com/typicode/husky), etc.
   Reference: https://zenn.dev/luvmini511/articles/ade1f0e4b64770

### ESLint

1. Install @cspell/eslint-plugin as a dev-dependency
    ```bash
    npm install --save-dev @cspell/eslint-plugin
    ```
2. Add to it to .eslintrc.json
    ```json
    "extends": ["plugin:@cspell/recommended"]
    ```
3. Example:
   ```json
   {
    "plugins": ["@cspell"],
    "rules": {
      "@cspell/spellchecker": ["warn", { "checkComments": false, "autoFix": false }]
      }
    }
    ```
