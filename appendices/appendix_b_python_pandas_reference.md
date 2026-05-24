# Παράρτημα Β: Σύντομη αναφορά Python και pandas

Το παράρτημα αυτό συγκεντρώνει βασικά μοτίβα Python και `pandas` που εμφανίζονται συχνά στα παραδείγματα του βιβλίου. Δεν αντικαθιστά την αναλυτική παρουσίαση των κεφαλαίων, αλλά λειτουργεί ως γρήγορη αναφορά όταν ο αναγνώστης δουλεύει με notebooks και πίνακες δεδομένων.

## Β.1 Βασικοί τύποι δεδομένων της Python

Οι πιο συνηθισμένοι τύποι δεδομένων που συναντάμε στα παραδείγματα είναι:

| Τύπος | Παράδειγμα | Περιγραφή |
|---|---|---|
| `int` | `42` | Ακέραιος αριθμός. |
| `float` | `3.14` | Πραγματικός αριθμός. |
| `str` | `"κείμενο"` | Συμβολοσειρά. |
| `bool` | `True` | Λογική τιμή, αληθής ή ψευδής. |
| `list` | `[1, 2, 3]` | Διατεταγμένη συλλογή τιμών. |
| `dict` | `{"city": "Athens"}` | Συλλογή ζευγών κλειδιού-τιμής. |
| `tuple` | `(1, 2)` | Αμετάβλητη διατεταγμένη συλλογή. |
| `set` | `{1, 2, 3}` | Συλλογή μοναδικών τιμών. |

Παράδειγμα:

```python
text = "καλή μέρα"
words = text.split()
info = {"text": text, "word_count": len(words)}
```

## Β.2 Μεταβλητές και συναρτήσεις

Μια μεταβλητή αποθηκεύει μια τιμή:

```python
city = "Athens"
age = 34
```

Μια συνάρτηση ομαδοποιεί κώδικα που εκτελεί μια συγκεκριμένη εργασία:

```python
def count_words(text):
    return len(text.split())

count_words("μία μικρή πρόταση")
```

Στα notebooks, οι συναρτήσεις είναι χρήσιμες όταν η ίδια λογική εφαρμόζεται σε πολλά παραδείγματα ή σε πολλές στήλες.

## Β.3 Συνθήκες και επανάληψη

Οι συνθήκες επιτρέπουν διαφορετική εκτέλεση ανάλογα με μια τιμή:

```python
if score >= 0.5:
    label = "positive"
else:
    label = "negative"
```

Η επανάληψη χρησιμοποιείται όταν θέλουμε να εφαρμόσουμε την ίδια ενέργεια σε πολλά στοιχεία:

```python
texts = ["πρώτο κείμενο", "δεύτερο κείμενο"]

for text in texts:
    print(len(text.split()))
```

Σε εργασίες με `pandas`, συχνά αποφεύγουμε τα ρητά `for` όταν υπάρχει διαθέσιμη διανυσματοποιημένη πράξη.

## Β.4 Λίστες και comprehensions

Μια λίστα μπορεί να μετασχηματιστεί με comprehension:

```python
texts = ["καλή μέρα", "ένα μικρό παράδειγμα"]
lengths = [len(text.split()) for text in texts]
```

Με συνθήκη:

```python
long_texts = [text for text in texts if len(text.split()) > 2]
```

Τα comprehensions είναι χρήσιμα για μικρούς μετασχηματισμούς, αλλά όταν τα δεδομένα βρίσκονται σε `DataFrame`, συνήθως προτιμάμε μεθόδους της `pandas`.

## Β.5 Εισαγωγή βιβλιοθηκών

Συνηθισμένες εισαγωγές:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

Η χρήση σύντομων ονομάτων, όπως `pd` για την `pandas`, είναι καθιερωμένη και κάνει τον κώδικα πιο σύντομο.

## Β.6 Δημιουργία DataFrame

Ένα `DataFrame` είναι πίνακας με γραμμές και στήλες:

```python
import pandas as pd

df = pd.DataFrame({
    "text": ["καλή μέρα", "δύσκολη άσκηση"],
    "label": ["positive", "negative"],
})
```

Οι στήλες έχουν ονόματα και κάθε γραμμή αντιστοιχεί συνήθως σε μία παρατήρηση ή ένα τεκμήριο.

## Β.7 Φόρτωση και αποθήκευση δεδομένων

Ανάγνωση CSV:

```python
df = pd.read_csv("data/examples.csv")
```

Αν το αρχείο έχει διαφορετικό διαχωριστικό:

```python
df = pd.read_csv("data/examples.tsv", sep="\t")
```

Αποθήκευση CSV:

```python
df.to_csv("outputs/clean_examples.csv", index=False)
```

Η επιλογή `index=False` αποφεύγει την αποθήκευση του δείκτη ως επιπλέον στήλης.

## Β.8 Πρώτη επιθεώρηση πίνακα

Συνηθισμένες εντολές πρώτης διερεύνησης:

```python
df.head()
df.tail()
df.shape
df.columns
df.dtypes
df.info()
df.describe()
```

Για κατηγορικές τιμές:

```python
df["label"].value_counts()
```

Για κενές τιμές:

```python
df.isna().sum()
```

## Β.9 Επιλογή στηλών και γραμμών

Επιλογή μίας στήλης:

```python
df["text"]
```

Επιλογή πολλών στηλών:

```python
df[["text", "label"]]
```

Επιλογή γραμμών με βάση θέση:

```python
df.iloc[0]
df.iloc[0:5]
```

Επιλογή γραμμών και στηλών με ετικέτες:

```python
df.loc[0, "text"]
df.loc[0:5, ["text", "label"]]
```

## Β.10 Φιλτράρισμα γραμμών

Φιλτράρισμα με μία συνθήκη:

```python
positive = df[df["label"] == "positive"]
```

Με δύο συνθήκες:

```python
filtered = df[
    (df["label"] == "positive") &
    (df["word_count"] > 5)
]
```

Στην `pandas`, οι σύνθετες συνθήκες χρειάζονται παρενθέσεις. Χρησιμοποιούμε `&` για «και» και `|` για «ή».

## Β.11 Νέες στήλες και μετασχηματισμοί

Προσθήκη στήλης με μήκος κειμένου:

```python
df["char_count"] = df["text"].str.len()
```

Προσθήκη στήλης με πλήθος λέξεων:

```python
df["word_count"] = df["text"].str.split().str.len()
```

Με `assign`:

```python
df = df.assign(
    char_count=df["text"].str.len(),
    word_count=df["text"].str.split().str.len(),
)
```

Η μέθοδος `assign` είναι χρήσιμη όταν θέλουμε να κρατήσουμε τον μετασχηματισμό ως μέρος αλυσίδας εντολών.

## Β.12 Κενές τιμές

Έλεγχος κενών τιμών:

```python
df.isna()
df.isna().sum()
```

Αφαίρεση γραμμών με κενές τιμές:

```python
df_clean = df.dropna()
```

Συμπλήρωση με σταθερή τιμή:

```python
df["label"] = df["label"].fillna("unknown")
```

Συμπλήρωση αριθμητικής στήλης με διάμεσο:

```python
df["word_count"] = df["word_count"].fillna(df["word_count"].median())
```

Η διαχείριση κενών τιμών είναι αναλυτική απόφαση. Δεν υπάρχει μία σωστή λύση για όλα τα προβλήματα.

## Β.13 Ταξινόμηση

Ταξινόμηση κατά μία στήλη:

```python
df_sorted = df.sort_values("word_count")
```

Φθίνουσα ταξινόμηση:

```python
df_sorted = df.sort_values("word_count", ascending=False)
```

Ταξινόμηση κατά πολλές στήλες:

```python
df_sorted = df.sort_values(["label", "word_count"])
```

## Β.14 Ομαδοποίηση με groupby

Πλήθος γραμμών ανά κατηγορία:

```python
df.groupby("label").size()
```

Μέση τιμή ανά κατηγορία:

```python
df.groupby("label")["word_count"].mean()
```

Πολλαπλές συναρτήσεις:

```python
df.groupby("label")["word_count"].agg(["count", "mean", "median"])
```

Ομαδοποίηση με περισσότερες από μία στήλες:

```python
df.groupby(["region", "label"])["word_count"].mean()
```

Το `groupby` είναι ένα από τα βασικότερα εργαλεία για περιγραφική ανάλυση.

## Β.15 Συνένωση και συγχώνευση πινάκων

Κάθετη συνένωση πινάκων με ίδιες στήλες:

```python
df_all = pd.concat([df_a, df_b], ignore_index=True)
```

Συγχώνευση με κοινό κλειδί:

```python
df_merged = df.merge(annotations, on="doc_id", how="left")
```

Συνηθισμένες τιμές της παραμέτρου `how`:

| Τιμή | Περιγραφή |
|---|---|
| `"inner"` | Κρατά μόνο τις γραμμές με αντιστοίχιση και στους δύο πίνακες. |
| `"left"` | Κρατά όλες τις γραμμές του αριστερού πίνακα. |
| `"right"` | Κρατά όλες τις γραμμές του δεξιού πίνακα. |
| `"outer"` | Κρατά όλες τις γραμμές και από τους δύο πίνακες. |

Μετά από συγχώνευση, ελέγχουμε πάντα αν δημιουργήθηκαν απρόσμενες κενές τιμές ή διπλότυπες γραμμές.

## Β.16 Αναδιάταξη πινάκων

Πίνακας συχνοτήτων με `pivot_table`:

```python
table = df.pivot_table(
    index="region",
    columns="label",
    values="text",
    aggfunc="count",
    fill_value=0,
)
```

Μετατροπή από wide σε long μορφή:

```python
long = df.melt(
    id_vars=["doc_id"],
    value_vars=["score_a", "score_b"],
    var_name="annotator",
    value_name="score",
)
```

Η long μορφή είναι συχνά πιο κατάλληλη για ομαδοποιήσεις και οπτικοποίηση.

## Β.17 Δείκτες και ιεραρχικοί δείκτες

Ορισμός στήλης ως δείκτη:

```python
df_indexed = df.set_index("doc_id")
```

Επαναφορά δείκτη:

```python
df_reset = df_indexed.reset_index()
```

Ιεραρχικός δείκτης:

```python
hier_df = df.set_index(["volume", "chapter", "subject"])
```

Επιλογή από ιεραρχικό δείκτη:

```python
hier_df.loc[1]
```

Οι ιεραρχικοί δείκτες είναι χρήσιμοι όταν οι παρατηρήσεις οργανώνονται σε επίπεδα, όπως τόμος, κεφάλαιο και θέμα.

## Β.18 Κειμενικές πράξεις σε στήλες

Η πρόσβαση `.str` επιτρέπει πράξεις συμβολοσειρών σε ολόκληρη στήλη:

```python
df["text"].str.lower()
df["text"].str.contains("λέξη")
df["text"].str.replace("παλιό", "νέο", regex=False)
df["text"].str.split()
```

Παράδειγμα κανονικοποίησης:

```python
df["text_norm"] = (
    df["text"]
    .str.lower()
    .str.strip()
)
```

Πλήθος χαρακτήρων και λέξεων:

```python
df["char_count"] = df["text"].str.len()
df["word_count"] = df["text"].str.split().str.len()
```

## Β.19 Εφαρμογή συνάρτησης σε στήλη

Με `apply`:

```python
def first_word(text):
    return text.split()[0] if text else ""

df["first_word"] = df["text"].apply(first_word)
```

Το `apply` είναι ευέλικτο, αλλά μπορεί να είναι πιο αργό από τις ενσωματωμένες μεθόδους της `pandas`. Όταν υπάρχει έτοιμη διανυσματοποιημένη μέθοδος, συνήθως την προτιμάμε.

## Β.20 Βασική οπτικοποίηση από DataFrame

Ραβδόγραμμα συχνοτήτων:

```python
df["label"].value_counts().plot.bar()
```

Ιστόγραμμα:

```python
df["word_count"].plot.hist(bins=30)
```

Με `matplotlib`:

```python
import matplotlib.pyplot as plt

df["word_count"].plot.hist(bins=30)
plt.xlabel("Πλήθος λέξεων")
plt.ylabel("Συχνότητα")
plt.show()
```

Οι οπτικοποιήσεις βοηθούν στον γρήγορο έλεγχο κατανομών, ακραίων τιμών και πιθανών προβλημάτων στα δεδομένα.

## Β.21 Συχνά λάθη

### Ξεχασμένες παρενθέσεις σε σύνθετο φίλτρο

Λάθος:

```python
df[df["label"] == "positive" & df["word_count"] > 5]
```

Σωστό:

```python
df[(df["label"] == "positive") & (df["word_count"] > 5)]
```

### Αλλαγές που δεν αποθηκεύονται

Πολλές μέθοδοι επιστρέφουν νέο `DataFrame` αντί να αλλάζουν το υπάρχον:

```python
df.dropna()
```

Αν θέλουμε να κρατήσουμε το αποτέλεσμα:

```python
df = df.dropna()
```

### Σύγχυση ανάμεσα σε θέση και ετικέτα

Το `iloc` χρησιμοποιεί αριθμητικές θέσεις:

```python
df.iloc[0]
```

Το `loc` χρησιμοποιεί ετικέτες δείκτη και ονόματα στηλών:

```python
df.loc[0, "text"]
```

### Απρόσεκτη συγχώνευση

Μετά από `merge`, ελέγχουμε:

```python
df_merged.shape
df_merged.isna().sum()
df_merged.duplicated().sum()
```

Η συγχώνευση μπορεί να αλλάξει το πλήθος γραμμών αν το κλειδί δεν είναι μοναδικό.

## Β.22 Μικρή λίστα ελέγχου για κάθε νέο dataset

Όταν ανοίγουμε ένα νέο dataset, είναι χρήσιμο να ελέγχουμε:

- Πόσες γραμμές και στήλες έχει;
- Ποιες είναι οι στήλες;
- Ποιοι είναι οι τύποι δεδομένων;
- Υπάρχουν κενές τιμές;
- Υπάρχουν διπλότυπες γραμμές;
- Ποιες είναι οι βασικές κατηγορικές συχνότητες;
- Ποιες είναι οι βασικές αριθμητικές κατανομές;
- Χρειάζεται κανονικοποίηση κειμένου;
- Χρειάζεται συγχώνευση με άλλο dataset;
- Μπορεί ο κώδικας να εκτελεστεί ξανά από την αρχή;

Ένα σύντομο αρχικό μοτίβο:

```python
df = pd.read_csv("data/examples.csv")

display(df.head())
print(df.shape)
display(df.dtypes)
display(df.isna().sum())
display(df.describe(include="all"))
```

Αυτή η πρώτη επιθεώρηση συχνά αποκαλύπτει τα σημαντικότερα πρακτικά ζητήματα πριν ξεκινήσει η κυρίως ανάλυση.
