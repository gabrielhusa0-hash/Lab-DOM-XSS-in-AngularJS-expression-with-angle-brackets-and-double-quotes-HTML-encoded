# Lab: DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

## 📚 Studijní materiál
Tento repozitář slouží jako můj osobní studijní zápisník a přehled řešení laboratoří z platformy **PortSwigger Web Security Academy**. Dokumentuji zde postupy, zranitelnosti a způsob jejich exploitationu pro budoucí reference a rozvoj znalostí v oblasti kybernetické bezpečnosti.

---

## 🛠️ Postup řešení laboratoře

1. **Zkoumání vstupu:** Do vyhledávacího pole na stránce jsem zkusil zadat běžný text (např. `abcd`) a odeslal ho, abych zjistil, jak stránka s vnořeným textem pracuje.
2. **Vložení payloadu:** Do vyhledávání jsem zadal speciální výraz s dvojitými složenými závorkami, které dokázaly obejít bezpečnostní filtry:
   ```text
   {{$on.constructor('alert(1)')()}}

# Proč použítý payload fungoval?

Oklamání filtru: Stránka sice hlídala a kódovala běžné znaky (jako zobáčky nebo uvozovky), ale na dvojité složené závorky {{ a }} zapomněla, protože je považovala za obyčejný text.

Zpracování v AngularJS: Jakmile AngularJS narazil na složené závorky, vzal jejich obsah a bezmyšlenkovitě ho spustil jako příkaz.

Spuštění kódu ($on.constructor('alert(1)')()): Část $on slouží jako odrazový můstek v systému, .constructor z textu vyrobí reálnou funkci a závorky () na konci zajistí její okamžité spuštění.