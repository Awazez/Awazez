```
                              ......
                          :-=+****+=---:
                       .=#%%%%%%%%##*****=:
                      =%@@@@@@%%%%%%###****+:
                    :#@@@@@@@%%%%%%%###*++++*=:.
                   :%@@@@@@@@@%%%%%#%##*++++++=:.
                  -#@@@@@@@@%%%%%%%%###**+++++=-.
                 .*@@@@@@@@@@%%%%%%%##%#**+++===:.
                 :*@@@@%%%%%%@@%%%%%%#*=--::---=-.
                 .+@%#==+++++*###**+=---===-::..-:
                  +=-*****+=+*+-=-:.-----::::---=:.
                  -+#@@*++=-=+#=##+:---===---=--+=-:
                 -+@#@@%###**%*#%%#+-==+****+===+=-:
                 =%%@#%%%%%%###@@%%+--:-=**+====+=:-
                 :#%@@%%##**#%%*#%*-.:.::=*##+====::
                  =#@@@@@%*##+=:-::..::.::.-+*=----.
                  :*%%@@%=-==++++=====--:::--+-::-:.
                  .*##%@*-=+#%%%%%%##*=---==*=:::::
                   =*###%%%@@%@%##=-=========:::::.
                   .+****%%@@@@%#++===++=--::::::.
                    :*++*#%%@%%%#*+++===-:..:::..
                     -*++#*++*##%*=++=--:...::...
                      +##**+---==--=--:....::..:
                     .*@%*+++====-==-::....:::--:
                    -=-%@%##++===-==-:::::------.
                   -*+--#@@%%###**++++========-:...
              ...:-**+--=+%@@@@@@@%%##*++++++-.:.......
           .=+=---+**#+=+==*%@@@@@@%%##****+-...::.   ..:
            .-===+%%%@#==-::=*%%@@@%%%##*+=:.--:-==--.
               .-+%#*=-::-::.:=+*#%%%##*=::+++=. .--.
                  ....::::-:-::::-=+**+-:.:=:.
                      .... .....::...:....
```

# Awazez

Security researcher, based in Caen, France. I hunt on YesWeHack (as `awazez`),
HackerOne, Bugcrowd and HackenProof.

I go after the plumbing rather than the product. The login page gets reviewed by
everyone; the fetcher that resolves a URL on the server's behalf usually does not.

### What I look for

**SSRF in the incidental fetcher.** Not the product's own `image_url` field — that
one is upload-presigned and hardened by now. The ones worth the time are the
accessories: SAML/OIDC metadata loaders, "test this connection" buttons, URL
importers, HTML-to-PDF renderers, calendar subscriptions. Nobody owns them.

**The validator, not the parser.** A URL allowlist that resolves the name once and
fetches it twice is a rebinding target. One that follows redirects is an oracle.
One that reads back the response body is a finding on its own.

**Cache and transport.** Unkeyed inputs, CRLF injection, request desync — on the
raw origins a CDN never got put in front of.

**Authorization boundaries.** Tenant isolation, scope of a token, what a user role
can reach once you stop clicking the UI that hides it.

### Public tooling

- **[ssrf-redirect-kit](https://github.com/Awazez/ssrf-redirect-kit)** — a
  one-click-deploy 302 redirect oracle for authorized SSRF testing. Your own
  domain, real TLS, and full control of the status code and `Location` header,
  for the validators that reject anything with a query string in it.

### Rules I work by

Scope is scope. I prove an abuse primitive at N=2 and leave the ceiling untested
on purpose. I report one vulnerability per report, and I write the report so it
can be read in five minutes.

### Elsewhere

- X — [@awazez](https://x.com/awazez)
