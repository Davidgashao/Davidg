# סקינר Finviz – אסטרטגיית EMA 9 + VWAP (גרף 3 דקות)

## האסטרטגיה (לפי הסרטון)
| שלב | כלל |
|---|---|
| אינדיקטורים | **VWAP** + **EMA 9** על גרף **3 דקות** |
| כניסה | ממש לפני / ברגע ש-EMA 9 חוצה את ה-VWAP (לונג: EMA9 חוצה מעל VWAP) |
| סטופ 1 | נר נסגר **דרך** ה-EMA 9 אחרי החצייה (לונג: סגירה מתחת ל-EMA9) |
| סטופ 2 | או הפסד של **25%–30%** בפוזיציה (רלוונטי לאופציות) |
| יציאה ברווח | מחזיקים כל עוד הנרות נסגרים מעל ה-EMA 9 (רוכבים על המהלך) |

> **חשוב:** Finviz לא יודע לחשב חציית EMA9/VWAP בגרף 3 דקות – הוא עובד על נתונים יומיים.
> לכן הסקינר **מוצא את המניות המתאימות** (תנועה, ווליום, נזילות), ואת **הטריגר** עצמו
> מחפשים בגרף 3 דקות (TradingView / ברוקר). לשם כך מצורף גם אינדיקטור Pine – `ema9_vwap_cross.pine`.

---

## סקינר 1 – מניות מומנטום (Small Caps רצות)
מתאים לגרפים שבסרטון – מניות שקופצות חזק עם ווליום חריג.

**קישור מוכן:**
```
https://finviz.com/screener.ashx?v=111&f=sh_avgvol_o500,sh_curvol_o1000,sh_float_u50,sh_price_1to20,sh_relvol_o2,ta_change_u5&o=-relativevolume
```

| פילטר ב-Finviz | ערך | למה |
|---|---|---|
| Price | $1 to $20 | טווח מחיר של מניות מומנטום |
| Change | Up 5% | המניה כבר בתנועה היום |
| Relative Volume | Over 2 | ווליום כפול מהרגיל = עניין |
| Current Volume | Over 1M | נזילות היום |
| Average Volume | Over 500K | נזילות בסיסית |
| Float | Under 50M | פלוט קטן = מהלכים חדים |
| מיון | Relative Volume (יורד) | החזקות ביותר למעלה |

## סקינר 2 – מניות לאופציות (נזילות, Mid/Large Cap)
הסטופ של 25%–30% מתאים בעיקר לאופציות – זה הסקינר לזה.

**קישור מוכן:**
```
https://finviz.com/screener.ashx?v=111&f=cap_midover,sh_avgvol_o2000,sh_opt_option,sh_price_o10,sh_relvol_o1.5,ta_change_u2,ta_sma20_pa&o=-relativevolume
```

| פילטר ב-Finviz | ערך | למה |
|---|---|---|
| Market Cap | +Mid (over $2bln) | אופציות נזילות עם ספרד צר |
| Option/Short | Optionable | חייב שיהיו אופציות |
| Price | Over $10 | |
| Average Volume | Over 2M | נזילות גבוהה |
| Relative Volume | Over 1.5 | פעילות מעל הרגיל |
| Change | Up 2% | תנועה תוך-יומית |
| 20-Day SMA | Price above SMA20 | מגמה עולה – מתאים ללונג/Calls |
| מיון | Relative Volume (יורד) | |

### גרסת שורט / Puts (אופציונלי)
אותו רעיון הפוך – EMA9 חוצה **מתחת** ל-VWAP:
```
https://finviz.com/screener.ashx?v=111&f=cap_midover,sh_avgvol_o2000,sh_opt_option,sh_price_o10,sh_relvol_o1.5,ta_change_d2,ta_sma20_pb&o=-relativevolume
```

---

## סדר עבודה יומי
1. **9:30–9:45 (שעון ניו יורק)** – פותחים את הסקינר, בוחרים 3–5 מניות עם הכי הרבה Rel Volume.
   (מתוך ישראל: 16:30–16:45 ברוב השנה.)
2. פותחים לכל אחת גרף **3 דקות** עם **VWAP** + **EMA 9** (או האינדיקטור המצורף).
3. מחכים שה-EMA 9 יתקרב / יחצה את ה-VWAP → **כניסה**.
4. **סטופ:** נר 3 דק' שנסגר דרך ה-EMA 9 אחרי החצייה, **או** ‎-25%‎ עד ‎-30%‎ בפרמיה.
5. מחזיקים כל עוד הנרות נסגרים בצד הנכון של ה-EMA 9.

## אינדיקטור TradingView
קובץ: `ema9_vwap_cross.pine`
TradingView → Pine Editor → מדביקים → Add to chart → גרף 3 דקות.
מסמן חציות (BUY / SELL), מסמן יציאה כשנר נסגר דרך EMA 9, וכולל התראות (Alerts)
כדי שלא תצטרך לשבת מול המסך.

---
⚠️ זה לא ייעוץ השקעות. רווח של $84K בסרטון הוא תוצאה נבחרת – בדוק את האסטרטגיה
בדמו / Paper Trading לפני כסף אמיתי.
