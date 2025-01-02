# TV Program karta (Vyhledávací)

Tato vlastní karta v Home Assistant slouží k vyhledávání a zobrazení aktuálních a nadcházejících TV pořadů na základě definovaných filtrů. Umožňuje uživatelům prohlížet TV program a hledat pořady podle klíčových slov, která jsou zahrnuta ve vyhledávání, nebo naopak vylučována. 
Tato karta je vytvořena pro práci s daty z integrace *[Tv-Program](https://github.com/jerod33/Tv-Program).* 

## Funkce:
- **Vyhledávání pořadů**: Zobrazuje aktuální a nadcházející pořady, které odpovídají definovaným filtrům.
- **Filtrace podle klíčových slov**: Pořady, které obsahují klíčová slova zadaná ve filtru, budou zobrazeny. 
- **Vylučování klíčových slov**: Pořady, které obsahují slova uvedená ve filtru pro vylučování, budou skryty.


**Poznámka**: Mezery před a za slovem mohou ovlivnit výsledky vyhledávání. Všechna hledaná a vyloučená slova musí být oddělena čárkami.

## Instalace

### Pomocí HACS

- Přidejte toto úložiště jako vlastní úložiště integrace a poté restartujte Home Assistant.
- V části **Nastavení** → **Zařízení a služby** přidejte integraci a vyhledejte „televizní průvodce“.

### Ručně

- Stáhněte si soubor `upcoming_tv_show.js` a umístěte ho do složky `www/upcoming-tv-show`.

Ujistěte se, že jste tuto kartu přidali do správy zdrojů [Lovelace](https://my.home-assistant.io/redirect/lovelace_resources/):

```yaml
resources:
  - url: /local/upcoming-tv-show/upcoming_tv_show.js
    type: module
```
Jakmile je zdroj přidán, můžete konfigurovat kartu ve svém Lovelace rozhraní. Použijte následující YAML konfiguraci pro přidání karty:

```yaml
type: custom:tv-show-card
entities:
  - sensor.epg_sensor_day_1
  - sensor.epg_sensor_day_2
  - sensor.epg_yesterday
  - sensor.epg_sensor_day_3
  - sensor.epg_sensor_day_4
  - sensor.epg_sensor_day_5
  - sensor.epg_sensor_day_6
include_helper: input_text.epg_search_query
exclude_helper: input_text.epg_exclude_query
```

## Konfigurační možnosti

- **`type`**: *(Povinné)* Musí být `custom:tv-show-card` pro načtení vlastní karty.
- **`entities`**: *(Povinné)* Musí být vypsány všechny sensory, které se mají prohledávat(platí pouze pro sensory TV-program integrace).
- **`include_helper`**: *(Povinné)* Klíčová slova pro hledání pořadů. Pořady, popisy pořadů, které tato klíčová slova obsahují, budou zobrazeny.
- **`exclude_helper`**: *(Volitelné)* Klíčová slova pro vyloučení pořadů. Pořady, popisy pořadů, které tato klíčová slova obsahují, budou vyloučeny.
