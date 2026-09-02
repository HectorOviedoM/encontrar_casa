# Cómo funciona el ranking

Este repo tiene **un solo archivo para decidir**: [RANKING.md](RANKING.md).

El resto (`data/`, `snapshots/`, el Excel de Drive) es respaldo. Si hay duda, gana `RANKING.md`.

---

## Qué estamos eligiendo

La mejor **casa a refaccionar en Córdoba Capital** para:

1. comprar (techo **USD 100.000**; hasta 110k solo si el lote/barrio lo paga)
2. obra liviana o media
3. vender (no es tesis de renta, aunque un depto anexo suma)

No entra: pozo, boleto solo, PH/indivisa, country, Cerro/Urca (se van de techo), casa ya reciclada al precio de salida.

---

## Dónde se anota cada cosa

| Archivo | Rol |
|---|---|
| **RANKING.md** (raíz) | Lista viva. Abrís este. |
| **COMO_FUNCIONA.md** (raíz) | Estas reglas. |
| `snapshots/YYYY-MM-DD_barrido.md` | Qué se vio ese día en portales. |
| `data/*.md` | Export del Excel (histórico). |
| Drive sheet nuevo | Planilla con fórmulas. ID `1Mx7AWebClNpMjrDmyjFgIYSfz3HOQLGA` |

Una casa nueva **no** genera un markdown propio. Entra como fila en `RANKING.md`.

---

## Filtro duro (antes del score)

Tiene que cumplir todo:

- Córdoba **Capital** (no Carlos Paz, no Villa Giardino, no “Santa Rita” de otro partido)
- Casa o casa+depto sobre lote. No depto solo.
- Ask ≤ 100k. 100–110k solo si queda en sección A después del score.
- Palabra o foto de reciclar / a remodelar / precio claramente bajo el comparable del barrio.
- Se puede apuntar en mapa (calle o al menos barrio real).

Si falla el filtro → no entra al ranking. Puede ir a un renglón de “ruido” en el snapshot del día.

---

## ID

Formato: **prefijo de barrio + número de 2 dígitos**.

| Prefijo | Barrio |
|---|---|
| J | Jardín |
| SD | San Daniel |
| SF / O03 | San Fernando |
| RV | Residencial Vélez |
| PV | Parque Vélez |
| PA | Parque Atlántica |
| PL | Parque Latino |
| AA | Alto Alberdi |
| AC | Alta Córdoba |
| SR | Santa Rita |
| SM | SMATA |
| IP | Iponá |
| GP | General Paz |

El número es correlativo. No se reusa si la casa cae: J28 caído sigue siendo J28. La próxima de Jardín es J30.

Si es el mismo aviso en dos portales = **un solo ID**. Se deja el link más estable (Zonaprop / RE/MAX).

---

## Score (0–100)

| Eje | Pts | Qué premia | Qué castiga |
|---|---:|---|---|
| Ubicación | 25 | Jardín, San Fernando, Vélez, Jockey, UNC | Alta Córdoba, Yofre, SMATA, periferia |
| Spread | 30 | (comparable − 4% venta) − (ask + 5% compra + obra) ≥ 15% | All-in ≥ comparable |
| Lote | 20 | Tierra ≥ 200 m², esquina, frente usable | Lote chico, PH, fondo de pasillo |
| Obra | 15 | Cosmética / media | Techo, humedad estructural, “casi pozo” |
| Papeles | 10 | Escritura, planos, calle clara | Sin calle, fracción, “consultar” |

Bandas:

- **≥ 70** → sección A. Visitar.
- **55–69** → sección B. Válida, no primera.
- **< 55** → sección C (barato / mala salida) o D (no es flip).

### Números de obra (hasta visitar)

Usar % del ask si los m² del aviso son lote, no cubiertos:

- liviana 12%
- media 22%
- pesada 35%

O USD/m² cubierto: 180 / 280 / 380.

Comparables de salida están al pie de `RANKING.md`. No inventar un techo de reventa de otro barrio.

---

## Cómo entra una casa nueva (checklist)

Cuando aparece un aviso en Zonaprop, Argenprop, La Voz, ML, RE/MAX, etc.:

1. **Filtro duro.** Si no pasa, snapshot nomas.
2. **¿Ya está?** Buscar calle / m² / precio en `RANKING.md`. Si es duplicado, actualizar ask y estado. No crear ID nuevo.
3. **ID nuevo** con la tabla de prefijos.
4. Estimar obra + comparable del **mismo** barrio.
5. Calcular los 5 ejes y el score.
6. Meter la fila en A, B, C o D.
7. Reordenar la columna `#` de mayor a menor score. Empate: gana mejor barrio de salida, después menor ask.
8. Estado `VIVO`. Fecha en la nota o en el snapshot del día.
9. Si cambia el #1 o el corto de 10, reescribir el párrafo “Ganador provisorio”.

Eso es todo. No tocar `data/` salvo que se exporte de nuevo el Excel.

---

## Estados

| Estado | Significa |
|---|---|
| VIVO | Se vio en un portal en el último barrido |
| WATCH | Estaba, hoy no salió. No borrar. Bajar del corto si lleva >14 días |
| CAIDO | Confirmado fuera de mercado |
| NO | Entró por error o dejó de ser flip (ya reciclada, PH, >110k sin spread) |

Las anomalías de precio (Jardín a 50k) van a “Caídas / anomalías a matar”. Si reaparecen con ficha seria, saltan a #1 hasta la visita.

---

## Qué no hace el ranking

- No reemplaza visita, abogado ni plomero.
- No rankea “me gusta el barrio”. Ubicación es liquidez de **salida**.
- No mezcla Santa Rita Capital con Carlos Paz.
- No usa USD/m² de deptos para tasar casas.

---

## Fuentes que se barren

Zonaprop, Argenprop, Mercado Libre, Clasificados La Voz, iCasas, Properati, Nestoria/Mitula, RE/MAX, JB Srur.  
Facebook Marketplace: solo si Héctor pega el link (no hay scrape).

Queries listas: `data/02_Queries.md`.
