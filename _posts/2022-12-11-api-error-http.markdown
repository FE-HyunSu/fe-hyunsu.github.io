---
layout: post
title: "π API Error (http)"
date: 2022-12-11
tags: [issue]
---

## π API ERROR (http)

- νλ‘μ νΈ μ§νμ€ μΈλΆ apiλ₯Ό μ°λνλ μμμμ λ‘μ»¬νκ²½μμ  μ΄μκ° μμμΌλ, μ€μ  λΌμ΄λΈ λ°°ν¬μ api ν΅μ μ νμ§ λͺ»νλ μ΄μκ° λ°μλμλ€.

### π μλ¬ λ΄μ©

```
Mixed Content: The page at '{url}' was loaded over HTTPS, but requested an insecure XMLHttpRequest endpoint '{url}'. This request has been blocked; the content must be served over HTTPS.
```

- https νμ΄μ§μμ http νΈμΆμ νμλ λ°μλλ μλ¬.
- httpsλ httpμ λ¬λ¦¬ λ³΄μμ΄ κ°νλ νλ‘ν μ½.
- httpsλ‘ ν΅μ μ νλμ€ httpλ‘ μ°κ²°μ΄ λ°μνλ©΄ httpsμ λ³΄μμ μ±μ μν΄μ block μ²λ¦¬ λλ€.
- http -> https μμ²­μ (O)
- https -> http μμ²­μ (X)

<br/>

### π» ν΄κ²° λ°©λ² 1

- νΈμΆ apiμ httpλ₯Ό https λ‘ λ³κ²½.
- λλ μλ meata νκ·Έλ₯Ό μΆκ°. (React νλ‘μ νΈλΌλ©΄ \_document.tsx)

```tsx
<meta
  http-equiv="Content-Security-Policy"
  content="upgrade-insecure-requests"
></meta>
```

<br/>

### π ν΄κ²° λ°©λ² 2

- ν΄κ²°λ°©λ² 1,2λ κ²°κ΅­ http μμ²­μ httpsλ‘ λ³ννμ¬ μμ²­νλ λ°©μμ΄λ€.
- httpνκ²½μμλ§ μ κ³΅λλ api λΌλ©΄ 'https://proxy.cors.sh' λ₯Ό μ΄μ©νμ¬, μ°ννμ¬ μ¬μ©μ΄ κ°λ₯.<br/>ex) https://proxy.cors.sh/http://{url}
- λ³΄μμ http μ£Όμμ api μμ²­μ μμ νλλ‘ νμ.

<br/>

---

<br/>

## π« μ°Έκ³  νμ΄μ§

- [https://github.com/swagger-api/swagger-ui/issues/1670](https://github.com/swagger-api/swagger-ui/issues/1670){:target="\_blank"}
- [https://cors.sh](https://cors.sh){:target="\_blank"}
  <br/><br/>

---
