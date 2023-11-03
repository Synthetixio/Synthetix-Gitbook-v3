# Introduction

{% hint style="info" %}
Perps V3 is in late stages of development, so minor changes and updates are possible
{% endhint %}

* Multi collateral: accepts any synths configured in the system as margin for an account
* Cross margin: account margin can be used across positions on markets
* Accounts with Role Based Access Control for modifying collateral, opening/closing positions
* Improved liquidations and no more endorsed liquidators
* Key limitations
  * Single position per market&#x20;
  * Single pending order
  * Only async (delayed offchain) orders
  * No cancellation of orders; once order is expired, a new order can be placed.

{% embed url="https://github.com/Synthetixio/synthetix-v3/tree/main/markets/perps-market" %}
