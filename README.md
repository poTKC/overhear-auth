# overhear-auth

[Overhear](https://github.com/poTKC) の Spotify ログイン（OAuth 2.0 Authorization Code + PKCE）用の中継ページです。
GitHub Pages で `https://potkc.github.io/overhear-auth/callback/` として公開します。

Spotify はリダイレクト先に https（またはループバック）しか認めないため、LAN 内の端末へ直接戻れません。
このページは Spotify から受け取ったクエリ文字列を、`state` に書かれた端末の LAN アドレスへそのまま転送します。

- `state` の形式: `<プライベート IPv4>:<ポート>~<ワンタイム値>`
- 転送先はプライベート IPv4（10/8、172.16/12、192.168/16）とポート 1024〜65535 に限ります。
- 認可コードは端末だけが持つ PKCE の検証値がないとトークンに交換できません。
- 外部スクリプトは読み込まず、Referer も送りません。
