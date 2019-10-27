---
title: Putting your money on locales - Nook 2018
separator: ---
verticalSeparator: -v-
revealOptions:
  transition: 'slide'
---

# Putting your money on locales

Du hast 5 Geld in der Schweitz<br />- wo ist dein Währungssymbol?

-v-

### Moin

- speaker: Jakob Runge [@sicarius](https://twitter.com/sicarius)
- slides: [github.com/runjak/nook2019](https://github.com/runjak/nook2019)
  AT CH NET | Review currency symbol position
  -v-

### Outline

- Moin & outline
- Prelude to tragedy
- Was war noch gleich ne locale?
- Welche Organisationen sind beteiligt?
- Wo kommt das Problem eigentlich her?
  - libc?
  - v8 -> icu!
  - source pls?
- Wie ist das Problem jetzt?
- Wie ist die Eskalation jetzt?

---

## Prelude to tragedy

---

Was war noch gleich ne Locale?

ur_IN pa_IN ta_LK

- ur: [Urdu](https://en.wikipedia.org/wiki/Urdu)
- pa: [Punjabi](https://en.wikipedia.org/wiki/Punjabi_language)
- ta: [Tamil](https://de.wikipedia.org/wiki/Tamil)
- IN: [India](https://en.wikipedia.org/wiki/India)
- LK: [Sri Lanka](https://en.wikipedia.org/wiki/Sri_Lanka)

-v-

Task definition

- …so I'm working in ecommerce and we recently expanded to include Switzerland.
- aaand we thought we could get clever on the currencies.
- aaaaaand we thought `let's NOT use the companys API here`.

> Hey there, please have a look at this ticket:
> `[#TES-8327] AT CH NET | Review currency symbol position`

-v-

Instead of the companys API we decided to use the Browsers API: `Number.toLocaleString`.

```javascript
(5).toLocaleString('fr-CH', { currency: 'CHF', style: 'currency' });
// Node v10.15.1:  'CHF 5.00'
// Node v12.1.0:   '5.00 CHF'
// Firefox 66.0.2: '5.00 CHF'
// Chrome 73.0.…:  '5.00 CHF'
// Safari 12.0.3:  '5.00 CHF'
// IE 11:          '5.00 fr.'
```

-v-

Standards, die mitspielen:

- Sprachcodes: [ISO 639](https://en.wikipedia.org/wiki/ISO_639)
  - Siehe nicht: Macrolanguages, Glottolog
- Ländercodes: [ISO 3166](https://en.wikipedia.org/wiki/ISO_3166)
  - Siehe nicht: `EU`
- Währungscodes: [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)
  - Siehe nicht: Cryptocurrencies (BTC vs. XBT), Minerale (XAU, XAG)
